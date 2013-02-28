---
layout: post
title: "Flite and Clunit Voices"
date: 2008-09-22
comments: false
---
I have been playing around with [Flite][0] lately, which is basically a way to take a FestVox voice built for Festival and convert it to C code which can then be compiled into one monolithic binary. Flite ships with the KAL diphone voice. However, I don't particularly care for this voice, and have been trying to convert the CMU CLB ARCTIC voice for use with flite. I followed the [guide][1], and the automated conversion went smoothly, but at runtime I got bad synthesis and errors like this:



    
    clunits: unit type "f" not found
    clunit_get_unit_index: can't find unit type f, using 0
    





After many hours of studying the flite code and the festival code, I finally discovered what the problem was. In festvox/cmu\_us\_clb\_arctic\_clunits.scm, there was a phone-to-clunit mapping function:



    
    (define (cmu_us_clb_arctic::clunit_name i)
      "(cmu_us_clb_arctic::clunit_name i)
    Defines the unit name for unit selection for us.  The can be modified
    changes the basic classification of unit for the clustering.  By default
    this we just use the phone name, but you may want to make this, phone
    plus previous phone (or something else)."
      (let ((name (item.name i)))
        (cond
         ((and (not cmu_us_clb_arctic::clunits_loaded)
           (or (string-equal "h#" name) 
               (string-equal "1" (item.feat i "ignore"))
               (and (string-equal "pau" name)
                (or (string-equal "pau" (item.feat i "p.name"))
                (string-equal "h#" (item.feat i "p.name")))
                (string-equal "pau" (item.feat i "n.name")))))
          "ignore")
         ((string-matches name "[aeiou].*")
          (string-append
           name
           (item.feat i "R:SylStructure.parent.stress")))
         ((string-equal name "pau")
          name)
         (t
          (string-append
           name
           (item.feat i "seg_onsetcoda"))))))
    





However, the converted C code contained just:



    
    static char *cmu_us_clb_arctic_unit_name(cst_item *s)
    {
        return cst_strdup(item_name(s));
    }
    





Not surprisingly, converting arbitrary Scheme code to C is outside the capabilities of the Flite conversion code. The code I replaced it with doesn't encompass all of the logic of the original, but appears to work fine:



    
    static char *cmu_us_clb_arctic_unit_name(cst_item *s)
    {
        const char *name = item_name(s);
        if (*name == 'a' || *name == 'e' || *name == 'i' || *name == 'o' || *name == 'u')
        {
          const char *stress = ffeature_string(s, "R:SylStructure.parent.stress");
          char *namey = cst_alloc(char, strlen(name) + strlen(stress) + 1);
          cst_sprintf(namey, "%s%s", name, stress);
          return namey;
        }
        else if (strcmp(name, "pau"))
        {
          const char *onsetcoda = ffeature_string(s, "seg_onsetcoda");
          char *namey = cst_alloc(char, strlen(name) + strlen(onsetcoda) + 1);
          cst_sprintf(namey, "%s%s", name, onsetcoda);
          return namey;
        }
    
        return cst_strdup(item_name(s));
    }
    





(Before you go emailing me, cst\_alloc terminates the process on allocation failure. This code uses the same patterns as elsewhere in the Flite code.)




And now I have a working Flite binary for this voice.



[0]: http://www.speech.cs.cmu.edu/flite/
[1]: http://www.speech.cs.cmu.edu/flite/doc/flite_8.html#SEC19
