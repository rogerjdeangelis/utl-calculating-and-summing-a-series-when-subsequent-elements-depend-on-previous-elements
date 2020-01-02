# utl-calculating-and-summing-a-series-when-subsequent-elements-depend-on-previous-elements
Calculating and summing a series when subsequent elements depend on previous elements
    Calculating and summing a series when subsequent elements depend on previous elements

    github
    https://tinyurl.com/vf8tx9z
    https://github.com/rogerjdeangelis/utl-calculating-and-summing-a-series-when-subsequent-elements-depend-on-previous-elements

    Problem

      Sum the first 5 elements in the series

      b0=0.5

      ____
      \
       \  b  = b  * a  / 3
       /   i    i-1  i
      /___
     i=1 to 4

    Looks like the limit may be 0.6?

    I think it adds 1/6 of the remaining difference (.6 - sum ) with each subsequent element?
    The limit is .6?
    Too lazy to file up SymPy.
                                                             i

    *_                   _
    (_)_ __  _ __  _   _| |_
    | | '_ \| '_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    ;
    data have;
     input a b;
    cards4;
     0.5  .5
     0.5  .
     0.5  .
     0.5  .
     0.5  .
    ;;;;
    run;quit;

    *           _
     _ __ _   _| | ___  ___
    | '__| | | | |/ _ \/ __|
    | |  | |_| | |  __/\__ \
    |_|   \__,_|_|\___||___/

    ;

    WORK.HAVE total obs=15

    B(n)   A      B    |  Rules   B
                       |
     0    0.5    0.5   |  B0     0.5          (initial value)
     1    0.5     .    |  B1     0.08333      0.5*0.5/3  - 1/12
     2    0.5     .    |  B2     0.01389      0.08333*.5/3
     3    0.5     .    |  B3     0.00231      0.01389*.5/3
     4    0.5     .    |  B4     0.00039      0.00231*.5/3
                                 -------
                          Sum    0.59992

     *            _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| '_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    ;

    Up to 40 obs WORK.WANT total obs=5

    B(n)     BPRE        B         SUM       A

     0     0.00000    0.50000    0.50000    0.5
     1     0.50000    0.08333    0.58333    0.5
     2     0.08333    0.01389    0.59722    0.5
     3     0.01389    0.00231    0.59954    0.5
     4     0.00231    0.00039    0.59992    0.5

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    * this will work for chaging A and B values;
    data want;
     retain bPre b sum 0;
     set have;
      * set initial value or compute bn;
      b=ifn(_n_=1, b, (bPre*lag(a)/3));
      sum=sum+b;
      output;
      bPre=b;
    run;

