## Global Custom Field Type Definitions and Constraints

`URL`

* string
* must start with http://
* must not have any whitespace

`Email`

* string
* must contain an @ symbol
* must not have any whitespace
* must be entirely lower case

`Date`

* string
* YYYY-MM-DD

`Timestamp`

* number (integer)
* Unix Timestamp in milliseconds

`UID` (Firebase User ID)

* string
* 28 case-sensitive alphanumeric characters

`DID` (Firebase Document ID)

* string
* 20 case-sensitive alphanumeric characters

`Timezone`

* string
* One of the timezones in the [moment-timezone](https://momentjs.com/timezone/docs/#/using-timezones/getting-zone-names/) list of US timezones
* Command that returns list of all US timezones: `moment.tz.zonesForCountry('US')`
* Possible Values:\
    `["America/Adak", "America/Anchorage", "America/Boise", "America/Chicago", "America/Denver", "America/Detroit", "America/Indiana/Indianapolis", "America/Indiana/Knox", "America/Indiana/Marengo", "America/Indiana/Petersburg", "America/Indiana/Tell_City", "America/Indiana/Vevay", "America/Indiana/Vincennes", "America/Indiana/Winamac", "America/Juneau", "America/Kentucky/Louisville", "America/Kentucky/Monticello", "America/Los_Angeles", "America/Menominee", "America/Metlakatla", "America/New_York", "America/Nome", "America/North_Dakota/Beulah", "America/North_Dakota/Center", "America/North_Dakota/New_Salem", "America/Phoenix", "America/Sitka", "America/Yakutat", "Pacific/Honolulu"]`

`Address`

* string
* Valid address from Google Places API

`Latitude`

* number (float)
* value is between -90 and +90

`Longitude`

* number (float)
* value is between -180 and +180

`WeeklyOffset`

* number (integer)
* value is between 0 and 604800000

`UserType`

* string
* Possible Values: `["researcher", "participant"]`

<!-- 9.  SurveyQuestionType
    * string
    * Possible Values: `["short", "long", "multiple", "checkboxes", "dropdown", "number", "email", "phone", "file", "link", "date", "time"]` -->