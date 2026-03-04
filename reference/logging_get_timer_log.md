# Get timer log

Return a log of all timed events as a data.table

## Usage

``` r
logging_get_timer_log(clear_log = FALSE, deindent = TRUE)
```

## Arguments

- clear_log:

  (`logical(1)`, default FALSE) Should the log be cleared afterwards?

- deindent:

  (`logical(1)`, default TRUE) Should leading whitespace be removed from
  timer messages?

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
