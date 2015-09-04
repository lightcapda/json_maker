# json_maker
For generating large amounts of semi-randomized json from templates

# Instructions
```
usage: json_maker [-h] [--copies COPIES] [--copy_sleep COPY_SLEEP]
                  [--length LENGTH] [--combine] [--whitespace] [--digits]
                  [--string_keyword STRING_KEYWORD]
                  [--integer_keyword INTEGER_KEYWORD]
                  [--time_keyword TIME_KEYWORD] [--filename FILENAME]
                  [--combined_json_key COMBINED_JSON_KEY]
                  json_template

This program generates randomized json structures from a template.  
These are the formatting keywords that can be included in a json template which gets fed to json_maker

    <<TYPE[NUM]:.LENGTH>> represents a random string to be replaced by json_maker. The formatting options are:

        'TYPE' - Indicates the type of random string to use, may be one of: ['string', 'integer', 'time']
            'string' - Random selected characters from the set of 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
                (character set may be manipulated with optional parameters)
            'integer' - Random selected characters from the set of '0123456789'
            'time' - Unique (within a second) floating point non-idempotent timestamp

        'NUM' - The occurance of the type.  Must be an integer between 0 and n.  All types of the same occurance will 
            be identical values, different occurances are likely to be different but not necessarily.
            Eg, "The <<string[0]>> said the car needed a new <<string[1]>>,
            but the <<string[0]>> didn't have any <<string[1]>>'s in stock" would replace both '1'
            occurances with the same value and both '0' occurances with the same value

        ':.LENGTH' [OPTIONAL] - Truncates the string to the given LENGTH of characters.
            time types will have a maximum length of 17
            All other characters have a maximum length of 100
            If not specified, string and integer types default to 100

            

positional arguments:
  json_template         json file to use as a template, must be properly
                        formatted json with exceptions, see --help for details

optional arguments:
  -h, --help            show this help message and exit
  --copies COPIES       Number of copies of json to generate from
                        json_template, default is 1
  --copy_sleep COPY_SLEEP
                        Sleep between multiple copies, useful to space out
                        <<time>> types. Default is 0.1 seconds
  --length LENGTH       Default (and max) length of random values, default is
                        100 characters
  --combine             Combines the number of json copies into a single json
                        file as a list of items. Default is false, in which
                        case multiple files are generated from the same
                        template, each with different randomized strings and a
                        number appended.
  --whitespace          Adds whitespace characters to randomized strings
  --digits              Adds the characters "0123456789" to randomized
                        strings, has no impact on integer types
  --string_keyword STRING_KEYWORD
                        Sets the string keyword for templates (see above),
                        default is string
  --integer_keyword INTEGER_KEYWORD
                        Sets the integer keyword for templates (see above),
                        default is integer
  --time_keyword TIME_KEYWORD
                        Sets the timestamp keyword for templates (see above),
                        default is time
  --filename FILENAME   Name of the filename of the json output created,
                        default is "output". If multiple copies are specified
                        and the --combine flag is not passed, a number will be
                        appended to the name
  --combined_json_key COMBINED_JSON_KEY
                        json key to use when multiple copies are combined into
                        a list, the default is output
```
