# Time and date


##**$.unixtime**()

Returns current time in unixtime GMT0 format. There are arithmetic arguments possible.

Examples:

    // Returns current time in unixtime

        $.unixtime()

    // Returns unixtime for current time + 60 min

        $.unixtime(%y-%m-%d %h:%i+60:%s)

    // Returns unixtime for current date with set time 02:00:00

        $.unixtime(%y-%m-%d 02:00:00)

##**$.date**(%y-%m-%d %h:%i:%s)

Convert date in 2015-02-04 16:19:33 fromat. There are arithmetic arguments possible.

Example:

    // Returns current date/time in format yyyy-MM-dd HH:mm:SS

        $.date(%y-%m-%d %h:%i:%s)

    // add +1 day to return date in format yyyy-MM-dd HH:mm:SS

        $.date(%y-%m-%d+1 %h:%i:%s)

