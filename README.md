
<!-- README.md is generated from README.Rmd. Please edit that file -->

# mscstts2

<!-- badges: start -->
<!-- badges: end -->

:exclamation:*mscstts2 is a reboot of
[mscstts](https://github.com/muschellij2/mscstts). Instead of
[httr](https://httr.r-lib.org/#status), which is superseded and not
recommended, we use [httr2](https://httr2.r-lib.org/) to perform HTTP
requests to the Microsoft Cognitive Services Text to Speech REST API.*

mscstts2 is a client to the Microsoft Cognitive Services Text to Speech
REST API. The Text to Speech REST API supports neural text to speech
voices, which support specific languages and dialects that are
identified by locale. Each available endpoint is associated with a
region.

Before you use the text to speech REST API, a valid account must be
registered at the [Microsoft Azure Cognitive
Services](https://azure.microsoft.com/en-us/free/cognitive-services/)
and you must obtain an API key. Without an API key, this package will
not work.

## Installation

You can install the development version of mscstts2 from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("howardbaek/mscstts2")
```

## Getting an API key

1.  Sign in/Create an Azure account on [Microsoft Azure Cognitive
    Services](https://azure.microsoft.com/en-us/free/cognitive-services/).
2.  Click `+ Create a resource`
3.  Search for “Speech” and Click `Create` -\> `Speech`
4.  Create a [Resource
    group](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/manage-resource-groups-portal#what-is-a-resource-group)
    and a “Name”.
5.  Choose `Pricing tier` (you can choose the free version with
    `Free F0`)
6.  Click `Review + create`, review the Terms, and click `Create`.

If the deployment was successful, you should see :white_check_mark:
**Your deployment is complete** on the next page.

7.  Under `Next steps`, click `Go to resource`
8.  Look on the left sidebar and under `Resource Management`, click
    `Keys and Endpoint`
9.  Copy either `KEY 1` or `KEY 2` to clipboard. Only one key is
    necessary to make an API call.

Once you complete these steps, you have successfully retrieved your API
keys to access the API.

On this page, jot down your `Location/Region`, which you use to make
calls to the API.

:warning: Using a different region from the region of your API key will
lead to errors when you make calls to the API.

## Setting your API key

You can set your API key in a number of ways:

1.  Edit `~/.Renviron` and set `MS_TTS_API_KEY = "XXXX"`
2.  In `R`, use `options(ms_tts_key = "XXXX")`.
3.  Set `export MS_TTS_API_KEY=XXXX` in `.bash_profile`/`.bashrc` if
    you’re using `R` in the terminal.
4.  Pass `api_key = "XXXX"` in arguments of functions such as
    `ms_list_voices(api_key = "XXXX")`.

## Get a list of voices

`ms_list_voice()` uses the
`tts.speech.microsoft.com/cognitiveservices/voices/list` endpoint to get
a full list of voices for a specific region. It attaches a region prefix
to this endpoint to get a list of voices for that region. For example,
to get a list of all the voices for the `westus` region, it uses the
`https://westus.tts.speech.microsoft.com/cognitiveservices/voices/list`
endpoint.

``` r
ms_list_voice()
```

## Convert text to speech

`ms_synthesize()` uses the
`tts.speech.microsoft.com/cognitiveservices/v1` endpoint to convert text
to speech. The endpoint requires Speech Synthesis Markup Language (SSML)
to specify the language, gender, and full voice name.

TODO: Warn users of HTTP 403 Forbidden Error :warning:

Be sure to select the endpoint that matches your Speech resource region.

``` r
ms_synthesize()
```

## Get an access token

`ms_get_token()` makes a request to the `issueToken` endpoint to get an
access token. The function require an API key and region as inputs.

``` r
ms_get_token()
```

## Major differences to mscstts

TODO: Elaborate on these differences

- httr -\> httr2
- Improved documentation
- Fixed HTTP 403 error

## Acknowledgements

mscstts2 wouldn’t be possible without mscstts by [John
Muschelli](https://github.com/muschellij2) and httr2 by [Hadley
Wickham](https://github.com/hadley).
