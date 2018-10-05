# Functions

Functions may be used in next logics: `Condition`, `Copy task`, `Call Process`, `API Call`, `Set Parameter`.

[Node parameters reading](getParamFromCount.md) -
returns value of counter of tasks in the node

[Parameters values](getParamFromApp.md) - returns value of task parameter from specified process

[Time and date](unixtime.md) - conversion and formatting of date/time

[Math](math.md) - return result of math actions (addition, subtraction, multiplication and division) of constants and/or parameters

**$.sha1_hex**(_content_) - returns sha1 in hex from constant or task parameter if it is specified in `{{parameter_name}}` format

**$.sha1**(_content_) - returns sha1 in hex from constant or task parameter if it is specified in `{{parameter_name}}` format

**$.base64_encode**(_content_) - convert constant or task parameter in base64 formatмат base64, if it is specified in `{{parameter_name}}` format

_content_ - constant or `{{parameter_name}}`