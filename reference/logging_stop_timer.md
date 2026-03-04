# End logging timer

End a nested timer

## Usage

``` r
logging_stop_timer(echo = TRUE)
```

## Arguments

- echo:

  (`logical(1)`, default = TRUE) Should the message be written to
  screen?

## Examples

``` r
mbg::logging_start_timer(msg = 'Test logging')
#> Error in loadNamespace(x): there is no package called ‘mbg’
Sys.sleep(0.1)
mbg::logging_stop_timer()
#> Error in loadNamespace(x): there is no package called ‘mbg’
log_results <- mbg::logging_get_timer_log()
#> Error in loadNamespace(x): there is no package called ‘mbg’
print(log_results)
#> Error: object 'log_results' not found
```
