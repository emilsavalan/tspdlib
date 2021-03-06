
kpss_1break
==============================================

Purpose
----------------

Computes the KPSS stationary test with one structural break.

Format
----------------
.. function:: {  kpss_stat, tb, lambda, cv } = KPSS_1break(y, model, bwl, varm, trimm)


    :param y: Time series data to be test.
    :type y: Nx1 matrix

    :param model: Model to be implemented.

          =========== ===========================
          1           Break in level.
          2           Break in level and trend.
          =========== ===========================

    :type model: Scalar

    :param bwl: Bandwidth for the spectral window.
    :type  bwl: Scalar

    :param varm: Long-run consistent variance estimation method

          =========== =====================================================
          1           iid.
          2           Bartlett.
          3           Quadratic Spectral (QS).
          4           SPC with Bartlett /see (Sul, Phillips & Choi, 2005)
          5           SPC with QS
          6           Kurozumi with Bartlett
          7           Kurozumi with QS
          =========== =====================================================

    :type varm: Scalar

    :param trimm: Trimming rate.
    :type trimm: Scalar

    :return kpss_stat: The KPSS test statistic.
    :rtype kpss_stat: Scalar

    :return tb: Location of break.
    :rtype tb: Scalar

    :return lambda: Break fraction (tb/T).
    :rtype lambda: Scalar

    :return cv: 1, 5, and 10 percent critical values for :func:`kpss_1break` statistic.
    :rtype cv: Vector

Examples
--------

::

  new;
  cls;
  library tspdlib;

  // Load date file
  y = loadd(__FILE_DIR $+ "TSe.dat");
  T = rows(y);

  // bandwidth lag
  bwl = round(4 * (T/100)^(2/9));

  // Trimming rate
  trimm = 0.10;

  /*
  ** 1 = Break in level
  ** 2 = Break in level and trend
  */
  model = 1;

  // Set long-run variance computation type
  // 1           iid.
  // 2           Bartlett.
  // 3           Quadratic Spectral (QS).
  // 4           SPC with Bartlett /see (Sul, Phillips & Choi, 2005)
  // 5           SPC with QS
  // 6           Kurozumi with Bartlett
  // 7           Kurozumi with QS
  varm = 1;

 { KPSS, tb1, lambda, cv } = KPSS_1break(y, model, bwl, varm, trimm);

Source
------

kpss_1br.src

.. seealso:: Functions :func:`lmkpss`, :func:`kpss_2break`
