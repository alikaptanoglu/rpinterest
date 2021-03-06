
<!-- README.md is generated from README.Rmd. Please edit that file -->

# `{rpinterest}`

The goal of rpinterest is to provide access to the Pinterest API from R.

`{rpinterest}` is designed to either retrieve data from Pinterest or to
post to your account from R. For exemple, you can share a dataviz made
in R to Pinterest (or any other file from your computer).

## Installation

You can install the released version of `{rpinterest}` from the
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("rpinterest")
```

Or for the dev version:

``` r
remotes::install_github("ColinFay/rpinterest", build_vignettes = TRUE)
```

## Getting an Access Token

Go to `https://developers.pinterest.com/apps/` and register a new app.
In this new app, use `https://colinfay.me/rpinterestcallback/` as a
callback URL. You can also use a custom callback if you build your own.
Read the Vignette “rpinterest-oauth” for more info about the why and the
how.

Once your app is set, use pinterest\_token to create a token:

``` r
token <- pinterest_token(
  app = "yourapp", 
  app_id = "yourappid", 
  app_secret = "yourappsecret"
)
```

You’ll be taken to a Pinterest login page and R will be waiting for a
connection code. After login, `https://colinfay.me/rpinterestcallback/`
will contain a code that you’ll need to paste back to R.

## About rate limit

If your pinterest app is unauthorised, you’ll be granted 10 requests per
hour per token.

## Call the API

### Interact with your profile

#### Get informations about the logged user

Get information about your account :

  - `get_logged_user()`, `get_logged_user_boards()`, and
    `get_logged_user_boards_suggestions()` return informations about
    yourself.

#### Interact with your account

##### Create

  - `create_board()` creates a board on your account, with a name and a
    description.
  - `create_pin()` creates a pin on one of your board, with a name and a
    description, from a local file.

##### Delete

  - `delete_board()` delete a board on your account.
  - `delete_pin()` delete on one of your pin.

##### Edit

  - `edit_board()` edit a board on your account, with a name and a
    description.
  - `edit_pin()` creates a pin on one of your board, with a name and a
    description, from a local file.

### Sending plots to Pinterest

`ggplot_to_pinterest()` sends a ggplot2 object to a Pinterest Board.
Note that `{ggplot2}` has to be installed to run this command.

``` r
library(ggplot2)
x <- ggplot(iris, aes(Sepal.Length, Sepal.Width)) + geom_point()
ggplot_to_pinterest(x, "colinfay/gris-mon-amour", "test rpinterest", token = token)
```

### Retrieve data from Pinterest

#### Boards

##### Pins

Get all the pins from a board:

  - by id

<!-- end list -->

``` r
get_board_pins_by_id(id = "42080646457333782", token = token)
```

  - by
name

<!-- end list -->

``` r
get_board_pins_by_name(user = "colinfay", board = "blanc-mon-amour", token = token)
```

##### Spec

  - by id

<!-- end list -->

``` r
get_board_spec_by_id(id = "42080646457333782", token = token)
```

  - by
name

<!-- end list -->

``` r
get_board_spec_by_name(user = "colinfay", board = "blanc-mon-amour", token = token)
```

#### Pins

##### Spec

``` r
get_pin_spec_by_id(id = "42080577745042298", token = "your_token")
```

#### User

##### Spec

  - by id

<!-- end list -->

``` r
get_user_spec_by_id(id = "42080715176677612", token = token)
```

  - by name

<!-- end list -->

``` r
get_user_spec_by_name(user = "colinfay", token = token)
```

## Code of Conduct

Please note that the ‘rpinterest’ project is released with a
[Contributor Code of Conduct](CODE_OF_CONDUCT.md). By contributing to
this project, you agree to abide by its terms.
