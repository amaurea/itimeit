itimeit: Ipython-like %timeit outside of ipython
=================================================

Use just like the magic %timeit in Ipython

    >from itimeit import itimeit
    >itimeit("1+1")
    10000000 loops, best of 3: 21.03 ns per loop

Can also specify a baseline to subtract. For example,
specifying `baseline="pass"` let's you apprximately compensate
for the time taken by the timing loop itself.

    >itimeit("1+1", baseline="pass")
    10000000 loops, best of 3: 4.367 ns per loop

Access locals, including functions and imported modules,
directly in the code to benchmark, without a cumbersome
setup step.

    >def foo(i):
      while i != 0:
        i /= 2
    >itimeit("foo(100)")
    1000000 loops, best of 3: 593.7 ns per loop

    >itimeit("np.random.standard_normal((1000,1000))")
    10 loops, best of 3: 72.01 ms per loop

The cost of this is that the environment is affected
when timing mutating commands.

    >a = np.arange(10)
    >def bar(a): a += 1
    1000000 loops, best of 3: 1.145 µs per loop
    >print a[0]
    3111111
