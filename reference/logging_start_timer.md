# Start logging timer

Start a nested timer with an optional message

## Usage

``` r
logging_start_timer(msg, echo = TRUE, indentation_text = "  ")
```

## Arguments

- msg:

  (`character(1)`) Logging message

- echo:

  (`logical(1)`, default TRUE) Should the message be written to screen?

- indentation_text:

  (`character(1)`, default " ") Text that will be repeated at the
  beginning of the message for each layer of indentation

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
