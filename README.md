# utl-select-only-numeric-variables-using-sql-in-r-python-and-sas-sql
Select only numeric variables using sql in r python and sas sql
    %let pgm=utl-select-only-numeric-variables-using-sql-in-r-python-and-sas-sql;

    Select only numeric variables using sql in r python and sas sql

        SOLUTIONS

            1 sas sql (same code in r, python and excel. Except dynamic python.

            2 r sql

            3 python sql(submit pyendx macro does not support
              dynamic execution due to triple quotes
              and forced indentation)

            4 base r

            5 python numpy and pandas language
              SOAPBOX ON
                Programmers can create python programs without inporting numpy and pandas but it seems rare
              SOAPBOX OFF

            6 excel sql not prsented here (see https://tinyurl.com/59rnt8ab )

    github
    https://tinyurl.com/bwbe6986
    https://github.com/rogerjdeangelis/utl-select-only-numeric-variables-using-sql-in-r-python-and-sas-sql

    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                                 |                               |                                                      */
    /*            INPUT                |          PROCESS              |       OUTPUT                                         */
    /*            =====                |          =======              |       ======                                         */
    /*                                 |                               |                                                      */
    /*                                 |                               |                                                      */
    /*   NAME   SEX AGE HEIGHT WEIGHT  |  1-3 SAS,PYTHON, R, EXCEL     |    AGE HEIGHT WEIGHT                                 */
    /*                                 |  EXCEPT DYNAMIC PYTHON        |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |   DYNAMIC CODE                |     14  69.0   112.5                                 */
    /*  Alfred   M   14  69.0   112.5  |   select                      |     13  56.5    84.0                                 */
    /*  Alice    F   13  56.5    84.0  |      %utl_varlist(            |     13  65.3    98.0                                 */
    /*  Barbara  F   13  65.3    98.0  |         sd1.have              |                                                      */
    /*                                 |        ,keep=_numeric_        |                                                      */
    /*  options                        |        ,od=%str(,))           |                                                      */
    /*    validvarname=upcase;         |   from                        |                                                      */
    /*  libname sd1 "d:/sd1";          |      sd1.have                 |                                                      */
    /*  data sd1.have;                 |                               |                                                      */
    /*   set                           |   SAS HARDCODED               |                                                      */
    /*    sashelp.class(obs=3);        |                               |                                                      */
    /*  run;quit;                      |    %put %utl_varlist(         |                                                      */
    /*                                 |       sd1.have                |                                                      */
    /*                                 |      ,keep=_numeric_          |                                                      */
    /*                                 |      ,od=%str(,)) ;           |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |    /*- copy from log -*/      |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |    select                     |                                                      */
    /*                                 |      AGE,HEIGHT,WEIGHT        |                                                      */
    /*                                 |    from                       |                                                      */
    /*                                 |      sd1.have                 |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |  4 base r                     |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |    want<-                     |                                                      */
    /*                                 |     Filter(is.numeric,have)   |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |  5 python numpy and pandas    |                                                      */
    /*                                 |      language                 |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |    import pandas as pd        |                                                      */
    /*                                 |    import numpy as np         |                                                      */
    /*                                 |    want =   \                 |                                                      */
    /*                                 |     have.select_dtypes  \     |                                                      */
    /*                                 |     (include=np.number) \     |                                                      */
    /*                                 |                               |                                                      */
    /*                                 |  6 excel sql see              |                                                      */
    /*                                 |  https://tinyurl.com/59rnt8ab |                                                      */
    /*                                 |                               |                                                      */
    /**************************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options
      validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     set
      sashelp.class(obs=3);
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   NAME      SEX    AGE    HEIGHT    WEIGHT                                                                             */
    /*                                                                                                                        */
    /*  Alfred      M      14     69.0      112.5                                                                             */
    /*  Alice       F      13     56.5       84.0                                                                             */
    /*  Barbara     F      13     65.3       98.0                                                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    /*---- SAS DYNAMIC ----*/

    proc sql;
      create
          table want as
      select
         %utl_varlist(
            sd1.have
           ,keep=_numeric_
           ,od=%str(,))
      from
         sd1.have
    ;quit;

    /*---- SAS HARDCODED ----*/

    %put %utl_varlist(
       sd1.have
      ,keep=_numeric_
      ,od=%str(,)) ;

    /*- copy from log -*/

    proc sql;
      create
          table want as
    select
      AGE,HEIGHT,WEIGHT
    from
      sd1.have
    ;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  AGE    HEIGHT    WEIGHT                                                                                               */
    /*                                                                                                                        */
    /*   14     69.0      112.5                                                                                               */
    /*   13     56.5       84.0                                                                                               */
    /*   13     65.3       98.0                                                                                               */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */

    /*---- R DYNAMIC ----*/

    /*---- CUT AND PASTE INTO SQLDF FROM THE LOG ----*/
    /*---- HERE IS WHAT IS IN THE LOG            ----*/

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source(
     "c:/oto/fn_tosas9x.R")
    have<-read_sas(
     "d:/sd1/have.sas7bdat")
    print(have)
    want<-sqldf('
      select
        %utl_varlist(sd1.have,keep=_numeric_,od=%str(,))
      from
        have
      ')
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /*---- R HARDCODED ----*/

    %put %utl_varlist(sd1.have,keep=_numeric_,od=%str(,));

    %let _numeric_ = %utl_varlist(sd1.have,keep=_numeric_,od=%str(,));

    /*---- CUT AND PASTE INTO SQLDF FROM THE LOG ----*/
    /*---- HERE IS WHAT IS IN THE LOG            ----*/

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source(
     "c:/oto/fn_tosas9x.R")
    have<-read_sas(
     "d:/sd1/have.sas7bdat")
    print(have)
    want<-sqldf("
      select
         AGE,HEIGHT,WEIGHT
      from
         have
         ")
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                       |                                                                                                 */
    /* > want                |  SAS                                                                                            */
    /*                       |                                                                                                 */
    /*   AGE HEIGHT WEIGHT   |  ROWNAMES    AGE    HEIGHT    WEIGHT                                                            */
    /*                       |                                                                                                 */
    /* 1  14   69.0  112.5   |      1        14     69.0      112.5                                                            */
    /* 2  13   56.5   84.0   |      2        13     56.5       84.0                                                            */
    /* 3  13   65.3   98.0   |      3        13     65.3       98.0                                                            */
    /*                       |                                                                                                 */
    /***************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */
    /*---- R HARDCODED ----*/

    %put %utl_varlist(sd1.have,keep=_numeric_,od=%str(,));

    %let _numeric_ = %utl_varlist(sd1.have,keep=_numeric_,od=%str(,));

    /*---- CUT AND PASTE INTO SQLDF FROM THE LOG ----*/
    /*---- HERE IS WHAT IS IN THE LOG            ----*/

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql('''
      select                 \
         AGE,HEIGHT,WEIGHT   \
      from                   \
         have                \
       ''');
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;

    /*  _     _
    | || |   | |__   __ _ ___  ___   _ __
    | || |_  | `_ \ / _` / __|/ _ \ | `__|
    |__   _| | |_) | (_| \__ \  __/ | |
       |_|   |_.__/ \__,_|___/\___| |_|

    */

    options
      validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     set
      sashelp.class(obs=3);
    run;quit;

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    source(
     "c:/oto/fn_tosas9x.R")
    have<-read_sas(
     "d:/sd1/have.sas7bdat")
    print(have)
    want<-
     Filter(is.numeric,have)
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                        |                                                                                               */
    /* > want                 |  SAS                                                                                          */
    /*                        |                                                                                               */
    /*     AGE HEIGHT WEIGHT  |  ROWNAMES    AGE    HEIGHT    WEIGHT                                                          */
    /*   <dbl>  <dbl>  <dbl>  |                                                                                               */
    /* 1    14   69     112.  |      1        14     69.0      112.5                                                          */
    /* 2    13   56.5    84   |      2        13     56.5       84.0                                                          */
    /* 3    13   65.3    98   |      3        13     65.3       98.0                                                          */
    /*                        |                                                                                               */
    /**************************************************************************************************************************/

    /*___                _   _                                                       ___                           _
    | ___|   _ __  _   _| |_| |__   ___  _ __    _ __  _   _ _ __ ___  _ __  _   _  ( _ )    _ __   __ _ _ __   __| | __ _ ___
    |___ \  | `_ \| | | | __| `_ \ / _ \| `_ \  | `_ \| | | | `_ ` _ \| `_ \| | | | / _ \/\ | `_ \ / _` | `_ \ / _` |/ _` / __|
     ___) | | |_) | |_| | |_| | | | (_) | | | | | | | | |_| | | | | | | |_) | |_| || (_>  < | |_) | (_| | | | | (_| | (_| \__ \
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |_| |_|\__,_|_| |_| |_| .__/ \__, | \___/\/ | .__/ \__,_|_| |_|\__,_|\__,_|___/
            |_|    |___/                                              |_|    |___/          |_|

    */

    options
      validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     set
      sashelp.class(obs=3);
    run;quit;

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    import pandas as pd
    import numpy as np
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want = have.select_dtypes(include=np.number)
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;

    proc datasets lib=sd1 nolist nodetails;
     delete want;
    run;quit;

    %utl_rbeginx;
    parmcards4;
    library(haven)
    library(sqldf)
    source(
     "c:/oto/fn_tosas9x.R")
    have<-read_sas(
     "d:/sd1/have.sas7bdat")
    print(have)
    import pandas as pd
    import numpy as np
    want =   \
     have.select_dtypes  \
     (include=np.number) \
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="want"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.want;
    run;quit;

    /**************************************************************************************************************************/
    /*                           |                                                                                            */
    /*  PYTHON                   |  SAS                                                                                       */
    /*                           |                                                                                            */
    /*      AGE  HEIGHT  WEIGHT  |  AGE    HEIGHT    WEIGHT                                                                   */
    /*                           |                                                                                            */
    /*  0  14.0    69.0   112.5  |   14     69.0      112.5                                                                   */
    /*  1  13.0    56.5    84.0  |   13     56.5       84.0                                                                   */
    /*  2  13.0    65.3    98.0  |   13     65.3       98.0                                                                   */
    /*                           |                                                                                            */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
