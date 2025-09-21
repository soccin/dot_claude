---
description: One-line will take nicely formatted R code and flatten everything to one line for easy copy pasting
allowed-tools: Read, Edit
---

# One-line

Reformat R code to allow for copy/pasting

Remove allowed newlines from the code. Eg any newlines that are within piped (`%>%` or `|>`) expressions. For example:
```
x = C %>%
  f(theta) %>%
  g(phi) %>%
  h(psi)
```
would become:
```
x = C %>% f(theta) %>% g(phi) %>% h(psi)
```

Similarly for ggplot chains:
```
ggplot(gistic_peaks, aes(x = gPos, y = 1 / q_values, color = type)) +
  theme_light() +
  geom_point() +
  scale_y_log10(expand = c(0, 0, 0, 0)) +
  geom_rect(
    data = chrom_panels,
    aes(xmin = xmin, xmax = xmax, ymin = ymin, ymax = ymax, fill = color),
    inherit.aes = FALSE,
    alpha = 0.2
  ) +
  ggsci::scale_fill_jama() +
  scale_x_continuous(expand = c(0, 0, 0, 0), breaks = NULL)
```
becomes
```
ggplot(gistic_peaks, aes(x = gPos, y = 1 / q_values, color = type)) + theme_light() + geom_point() + scale_y_log10(expand = c(0, 0, 0, 0)) + geom_rect(data = chrom_panels, aes(xmin = xmin, xmax = xmax, ymin = ymin, ymax = ymax, fill = color),inherit.aes = FALSE,alpha = 0.2) + ggsci::scale_fill_jama() + scale_x_continuous(expand = c(0, 0, 0, 0), breaks = NULL)
```

And for function defs; this,
```
is_integer <- function(x) {
  grepl("^-?[0-9]+$", x)
}
```
becomes
```
is_integer <- function(x) { grepl("^-?[0-9]+$", x) }
```

Try to make the code as compact as possible

Do not create invalid code

Do not change the code in ANY way other than removing newlines.

