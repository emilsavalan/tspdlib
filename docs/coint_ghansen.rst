coint_ghansen
==============================================

Purpose
----------------

Tests for the null of no cointegration against the alternative of cointegration with a structural break in the mean.

Format
----------------
.. function:: { ADF_min, TBadf, Zt_min, TBzt, Za_min, TBza, cvADFZt, cvZa } = coint_ghansen(y, x, model, bwl, ic, pmax, varm, trimm);


    :param y: Dependent variable.
    :type y: Nx1 matrix

    :param x: Independent variable.
    :type x: NxK matrix

    :param model: Model to be implemented.

          =========== ==============
          1           C   (level shift)
          2           C/T (level shift with trend)
          3           C/S (regime shift)
          4           Regime and trend shift
          =========== ==============

    :type model: Scalar

    :param bwl: Bandwidth length for long-run variance computation.
    :type bwl:  Scalar

    :param ic: The information criterion used for choosing lags.

         =========== ======================
         1           Akaike.
         2           Schwarz.
         3           t-stat significance
         =========== ======================

    :type ic: Scalar

    :param pmax: Maximum number of lags for Dy in ADF test.
    :type pmax: Scalar

    :param varm: Long-run consistent variance estimation method

             =========== ======================================================
             1           iid.
             2           Bartlett.
             3           Quadratic Spectral (QS).
             4           SPC with Bartlett /see (Sul, Phillips & Choi, 2005)
             5           SPC with QS
             6           Kurozumi with Bartlett
             7           Kurozumi with QS
             =========== ======================================================

    :type varm: Scalar

    :param trimm: Trimming rate.
    :type trimm: Scalar

    :return ADFmin: ADF test statistic
    :rtype ADFmin: Scalar

    :return TBadf: Break point using OLS.
    :rtype TBadf: Scalar

    :return Zamin: Za test statistic
    :rtype Zamin: Scalar

    :return TBza: Break point for using Za statistic.
    :rtype TBza: Scalar

    :return Ztmin: Zt test statistic
    :rtype Ztmin: Scalar

    :return TB_zt: Break point using Zt statistic.
    :rtype TB_zt: Scalar

    :return cvADFZt: 1%, 5%, 10% critical values for ADF and Zt test statistics.
    :rtype cvADFZt: Scalar

    :return cvZa:  1%, 5%, 10% critical values for Za test statistics.
    :rtype cvZa: Scalar


Examples
--------

::

  new;
  cls;
  library tspdlib;

  // Load the data
  data = loadd(__FILE_DIR $+ "TScoint.dat");

  // Define y and x matrix
  y = data[., 1];
  x = data[., 2:cols(data)];

  T = rows(data);

  /*
  ** Information Criterion:
  ** 1=Akaike;
  ** 2=Schwarz;
  ** 3=t-stat sign.
  */
  ic = 2;

  //Maximum number of lags
  pmax = 12;

  // Trimming rate
  trimm= 0.10;

  // Long-run consistent variance estimation method
  varm = 3;

  // Bandwidth for kernel estimator
  bwl = round(4 * (T/100)^(2/9));

  // Level shift
  model = 1;

  { ADF_min, TBadf, Zt_min, TBzt, Za_min, TBza, cvADFZt, cvZa } =
      coint_ghansen(y, x, model, bwl, ic, pmax, varm, trimm);


Source
------

coint_ghansen.src

.. seealso::
