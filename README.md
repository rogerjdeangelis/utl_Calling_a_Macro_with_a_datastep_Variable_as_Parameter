# utl_Calling_a_Macro_with_a_datastep_Variable_as_Parameter
Calling a Macro with Datastep Variables as Parameters.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.


    Calling a Macro with Datastep Variables as Parameters

    Printing three pages with page numbering("page m of n") consisting of students from sashelp.class.
    Also create a log dataset with error checking.
    This also shows the power of mete data.

    see
    https://communities.sas.com/t5/Base-SAS-Programming/Calling-a-Macro-with-Macro-Variable-as-Parameter/m-p/463707


    INPUT
    =====

     sashelp.class

     %macro prnt(name);
       proc print data=sashelp.class(where=(name="&name"));
       run;quit;
     %mend prnt;\


    PROCESS
    =======

    data log;

      array nams[3]  $8 ("Alfred","Alice","John");

      call symputx("pges",dim(nams));   * number of pages;

      do pge=1 to dim(nams);

        call symputx("name",nams[pge]);
        call symputx("pge",pge);  * page number;

        rc=dosubl('
           title "&name      Page &pge of &pges";
           %prnt(&name);
        ');

        if rc=0 then do;
            status="Completed";
            name=nams[pge];
        end;
        else status="Failed";
        output;

        keep name pge rc status;
      end;

    run;quit;

    OUTPUT
    ======

    Up to 40 obs from log total obs=3

    Obs    PGE    RC     STATUS       NAME

     1      1      0    Completed    Alfred
     2      2      0    Completed    Alice
     3      3      0    Completed    John


    Alfred      Page 1 of 3

    Obs     NAME     SEX    AGE    HEIGHT    WEIGHT

      1    Alfred     M      14      69       112.5


    Alice      Page 2 of 3

    Obs    NAME     SEX    AGE    HEIGHT    WEIGHT

      2    Alice     F      13     56.5       84


    John      Page 3 of 3

    Obs    NAME    SEX    AGE    HEIGHT    WEIGHT

     10    John     M      12      59       99.5


    *                _          _                   _
     _ __ ___   __ _| | _____  (_)_ __  _ __  _   _| |_ ___
    | '_ ` _ \ / _` | |/ / _ \ | | '_ \| '_ \| | | | __/ __|
    | | | | | | (_| |   <  __/ | | | | | |_) | |_| | |_\__ \
    |_| |_| |_|\__,_|_|\_\___| |_|_| |_| .__/ \__,_|\__|___/
                                       |_|
    ;

     sashelp.class

     %macro prnt(name);
       proc print data=sashelp.class(where=(name="&name"));
       run;quit;
     %mend prnt;\

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see process

