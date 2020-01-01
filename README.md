# utl-execute-a-macro-for-eash-word-in-a-macro-list
Execute a macro for eash word in a macro list
    Execute a macro for eash word in a macro list

    github
    https://tinyurl.com/w595f48
    https://github.com/rogerjdeangelis/utl-execute-a-macro-for-eash-word-in-a-macro-list

    macros
    https://tinyurl.com/y9nfugth
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    SAS forum
    https://tinyurl.com/wpt3fkz
    https://communities.sas.com/t5/SAS-Programming/Run-Macro-automatically-for-each-argument-in-ListValues-macro/m-p/614568

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;

    %macro putem(dte);
      dte=d&dte;output;
    %mend putem;

    %let lst=20191201 20191202 20191213 20191217 20191228;

    *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;


    WORK.WANT total obs=5

    Obs      DATES

     1     d20191201
     2     d20191202
     3     d20191213
     4     d20191217
     5     d20191228

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %let lst=20191201 20191202 20191213 20191217 20191228;

    %macro putem(dte);
      dates="d&dte";output;
    %mend putem;

    %array(dtes,values=&lst);

    * solution;

    data want;
      %dO_OVER(dtes, phrase=?,macro=putem);
    run;quit;
    *_              _
    | |_ ___   ___ | |___
    | __/ _ \ / _ \| / __|
    | || (_) | (_) | \__ \
     \__\___/ \___/|_|___/

    ;

    * get generated statements;

    data;
    file print;
      %do_over(dtes,phrase=%str(put "dates='d?';") ;);
    run;quit;

    dates='d20191201';
    dates='d20191202';
    dates='d20191213';
    dates='d20191217';
    dates='d20191228';


    * remove the macro array;

    %macro arraydelete(pfx)/des="Delete array macrovariables create by array macro";
      %do i= 1 %to &&&pfx.n;
          %symdel &pfx&i;
      %end;
    %mend arraydelete;

    %arraydelete(dtes);


