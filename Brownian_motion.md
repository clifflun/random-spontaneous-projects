Brownian Motion
================

## Simple Random Walk

Imagine a point that starts at (0,0) on a grid.

The point moves along the y-axis. There is a 50% chance that it moves up
(+1) and 50% chance down (-1).

Theoratically, the expected value should be 0 as the chances of moving
up and down are exactly the same, 50%.

However, reality shows that that will often not be the case. The
distribution seems completely random.

Below is a histogram showing the distribution frequency of where the
point lands on the number line after 10 ***thousand*** steps.

Even though the peak might not be at or near 0, these peaks resemble the
normal distribution curve.

``` r
## define plot data

set.seed(520)
n = 10000

ts = cumsum(sample(c(-1,1), n, replace = T))

rw = data.frame(ts, n = 1:length(ts), f = 1:n)

p <- ggplot(rw, aes(x=n, y=ts)) + 
  geom_line() + 
  geom_point(x=rw$n[1],y=ts[1], col = "green") +
  geom_point(x=tail(rw$n, 1),y=tail(ts,1), col = "red") +
  ggtitle("Simple Random Walk")

p
```

![](Brownian_motion_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

``` r
his <- ggplot(rw, aes(ts)) + 
  geom_histogram(binwidth = 1) + 
  ggtitle("Histogram of cumulative sum")

his
```

![](Brownian_motion_files/figure-gfm/unnamed-chunk-1-2.png)<!-- -->

## 2D random walk

The same principal but it happens on 2 different axis at the same time.

``` r
set.seed(520)
n = 25000


tx = cumsum(sample(c(-1,1), n, replace = T))
ty = cumsum(sample(c(-1,1), n, replace = T))

rw = data.frame(tx,ty)

p <- ggplot(rw, aes(tx,ty)) +
  geom_path() + 
  coord_fixed(1) +
  geom_point(x=tx[1],y=ty[1], col = "green") +
  geom_point(x=tail(tx, 1),y=tail(ty,1), col = "red") + 
  ggtitle("2D random walk")

p
```

![](Brownian_motion_files/figure-gfm/unnamed-chunk-2-1.png)<!-- -->

## Brownian motion (3D random walk)

Random particle path. Knitr is having trouble displaying interactive
plotly graphs, below is a screenshot of the 3D random walk.

``` r
set.seed(520)
n = 5000


tx = cumsum(sample(c(-1,1), n, replace = T))
ty = cumsum(sample(c(-1,1), n, replace = T))
tz = cumsum(sample(c(-1,1), n, replace = T))

rw = data.frame(tx,ty,tz,c = 1:n)

p <- plot_ly(rw, x=~tx, y=~ty, z=~tz, type="scatter3d", mode = "lines", line = list(width = 3, color = ~c, colorscale = 'Viridis'))
p
```

![3Drw](Brownian_motion_files/3D_rw.png)
