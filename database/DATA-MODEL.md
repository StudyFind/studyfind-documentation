# Document Paths and Structures

## Table of Contents

* [Researcher Document](#researcher-document)
* [Researcher Notification Document](#researcher-notification-document)
* [Participant Document](#participant-document)
* [Participant Notification Document](#participant-notification-document)
* [Study Document](#study-document)
* [Study Participant Document](#study-participant-document)
* [Note Document](#note-document)
* [Message Document](#message-document)
* [Meeting Document](#meeting-document)
* [Reminder Document](#reminder-document)
* [Mailing Document](#mailing-document)
* [Feature Document](#feature-document)
* [Bug Document](#bug-document)

## Researcher Document

```ts
// DOCUMENT PATH: /researchers/{researcherID}

{
  organization: string,
  background: string,
  phone: Phone,
  timezone: {
      region: Timezone,
      autodetect: boolean,
      updatedAt: Timestamp,
  },
  notifications: {
      local: boolean,
      email: boolean,
      phone: boolean,
  },
  createdAt: Timestamp,
  updatedAt: Timestamp,
}

```

| Name                  | Type        | Default           | Immutable | Notes                                                         |
|-----------------------|-------------|-------------------|-----------|---------------------------------------------------------------|
| `background`          | `string`    | ""                | false     | must be between 0 and 500 characters                          |
| `phone`               | `Phone`     | ""                | false     | must be a 10 digit string with exclusively numeric characters |
| `timezone.region`     | `Timezone`  | *set at creation* | false     | must be a valid US timezone from moment-timezone              |
| `timezone.autodetect` | `boolean`   | `true`            | false     | -                                                             |
| `timezone.updatedAt`  | `Timestamp` | *set at creation* | false     | time at which the timezone was last updated                   |
| `notifications.local` | `boolean`   | `true`            | false     | -                                                             |
| `notifications.email` | `boolean`   | `false`           | false     | -                                                             |
| `notifications.phone` | `boolean`   | `false`           | false     | -                                                             |
| `createdAt`           | `Timestamp` | *set at creation* | true      | time at which user was created                                |
| `updatedAt`           | `Timestamp` | *set on update*   | false     | time at which user was last updated                           |

---

## Researcher Notification Document

```ts
// CUSTOM TYPES

type ResearcherNotificationCode = "CREATE_ACCOUNT" | "DELETE_ACCOUNT" | "CREATE_STUDY" | "DELETE_STUDY" | "PARTICIPANT_ENROLLED" | "PARTICIPANT_CONFIRMED_MEETING" | "PARTICIPANT_CONFIRMED_REMINDER" | "MEETING_NOW"
```

```ts
// DOCUMENT PATH: /researchers/{researcherID}/notifications/{notificationID}

{
  title: string,
  body: string,
  link: URL,
  read: boolean,
  code: ResearcherNotificationCode,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}

```

| Name        | Type                         | Default           | Immutable | Notes                                                                                |
|-------------|------------------------------|-------------------|-----------|--------------------------------------------------------------------------------------|
| `title`     | `string`                     | *set at creation* | true      | -                                                                                    |
| `body`      | `string`                     | *set at creation* | true      | -                                                                                    |
| `link`      | `URL`                        | *set at creation* | true      | redirect link to relevant content on notification click                              |
| `read`      | `boolean`                    | `false`           | false     | has notification  been read by the user (can only be changed from `false` to `true`) |
| `code`      | `ResearcherNotificationCode` | *set at creation* | true      | determines notification type, icon, and color                                        |
| `createdAt` | `Timestamp`                  | *set at creation* | true      | time at which notification was sent                                                  |
| `updatedAt` | `Timestamp`                  | *set on update*   | false     | time at which notification was read                                                  |

---

## Participant Document

```ts
// CUSTOM TYPES

type BiologicalSex = "" | "Male" | "Female"
```

```ts
// DOCUMENT PATH: /participants/{participantID}

{
  sex: BiologicalSex,
  birthdate: Date,
  availability: string,
  phone: Phone,
  enrolled: DocumentID[],
  saved: DocumentID[],
  timezone: {
      region: Timezone,
      autodetect: boolean,
      updatedAt: Timestamp,
  },
  location: {
      address: Address,
      coordinates: {
          latitude: Latitude,
          longitude: Longitude,
      },
      autodetect: boolean,
      updatedAt: Timestamp,
  },
  notifications: {
      local: boolean,
      email: boolean,
      phone: boolean,
  },
  createdAt: Timestamp,
  updatedAt: Timestamp,
}

```

| Name                  | Type            | Default           | Immutable | Notes                                                                                            |
|-----------------------|-----------------|-------------------|-----------|--------------------------------------------------------------------------------------------------|
| `sex`                 | `BiologicalSex` | `""`              | false     | -                                                                                                |
| `birthdate`           | `Date`          | `""`              | false     | -                                                                                                |
| `availability`        | `string`        | `""`              | false     | must be between 0 and 500 characters                                                             |
| `phone`               | `Phone`         | ""                | false     | must be a 10 digit string with exclusively numeric characters                                    |
| `enrolled`            | `DocumentID[]`  | []                | true      | list of studyIDs the participant has enrolled for (updated solely by maintenance cloud fuctions) |
| `saved`               | `DocumentID[]`  | []                | false     | list of studyIDs the participant has saved                                                       |
| `timezone.region`     | `Timezone`      | *set at creation* | false     | must be a valid US timezone from moment-timezone                                                 |
| `timezone.autodetect` | `boolean`       | `true`            | false     | -                                                                                                |
| `timezone.updatedAt`  | `Timestamp`     | *set at creation* | false     | time at which the timezone was last updated                                                      |

| `location.address`              | `Address`       | *set at creation* | false     | must be a valid address from Google Places API                                                   |
| `location.coordinates.latitude` | `Latitude`      | *set at creation* | false     | -                                                                                                |
| `location.coordinates.longitude` | `Longitude`     | *set at creation* | false     | -                                                                                                |
| `location.autodetect`           | `boolean`       | `false`           | false     | -                                                                                                |
| `location.updatedAt`  | `Timestamp` | *set at creation* | false     | time at which the location was last updated                   |

| `notifications.local`           | `boolean`       | `true`            | false     | -                                                                                                |
| `notifications.email`           | `boolean`       | `false`           | false     | -                                                                                                |
| `notifications.phone`           | `boolean`       | `false`           | false     | -                                                                                                |
| `createdAt`                     | `Timestamp`     | *set at creation* | true      | time at which user was created                                                                   |
| `updatedAt`                     | `Timestamp`     | *set on update*   | false     | time at which user was last updated                                                              |


---

## Participant Notification Document

```ts
// CUSTOM TYPES

type ParticipantNotificationCode = "CREATE_ACCOUNT" | "DELETE_ACCOUNT" | "RESEARCHER_SENT_MESSAGE" | "RESEARCHER_CREATED_MEETING" | "RESEARCHER_UPDATED_MEETING" | "RESEARCHER_DELETED_MEETING" | "RESEARCHER_CREATED_REMINDER" | "RESEARCHER_UPDATED_REMINDER" | "RESEARCHER_DELETED_REMINDER" | "RESEARCHER_CHANGED_PARTICIPANT_STATUS" | "MEETING_NOW" | "REMINDER_NOW"
```

```ts
// DOCUMENT PATH: /participants/{participantID}/notifications/{notificationID}

{
  title: string,
  body: string,
  link: URL,
  read: boolean,
  code: ParticipantNotificationCode,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}

```

| Name        | Type                          | Default           | Immutable | Notes                                                                                |
|-------------|-------------------------------|-------------------|-----------|--------------------------------------------------------------------------------------|
| `title`     | `string`                      | *set at creation* | true      | -                                                                                    |
| `body`      | `string`                      | *set at creation* | true      | -                                                                                    |
| `link`      | `URL`                         | *set at creation* | true      | redirect link to relevant content on notification click                              |
| `read`      | `boolean`                     | `false`           | false     | has notification  been read by the user (can only be changed from `false` to `true`) |
| `code`      | `ParticipantNotificationCode` | *set at creation* | true      | determines notification type, icon, and color                                        |
| `createdAt` | `Timestamp`                   | *set at creation* | true      | time at which notification was sent                                                  |
| `updatedAt` | `Timestamp`                   | *set on update*   | false     | time at which notification was read                                                  |

---

## Study Document

```ts
// CUSTOM TYPES

type StudySex = "All" | "Male" | "Female"

type StudyType = "Observational" | "Interventional"

type StudyLocation = {
  address: Address,
  coordinates: {
    latitude: Latitude,
    longitude: Longitude,
  },
}

type StudyQuestionType = "Inclusion" | "Exclusion"
type StudyQuestionWeight = "Critical" | "High" | "Medium" | "Low" | "Trivial" | "Optional";

type StudyQuestion = {
  type: StudyQuestionType,
  weight: StudyQuestionWeight,
  prompt: string,
}

type StudyResource = {
  name: string, // resource name
  link: URL,
}
```

```ts
// DOCUMENT PATH: /studies/{studyID}

{
  activated: boolean,
  title: string,
  description: string,
  sex: StudySex,

  minAge: number,
  maxAge: number,
  acceptsHealthyParticipants: boolean,
  acceptsRemoteParticipants: boolean,
  type: StudyType,

  researcher: {
    id: UserID,
    name: string,
    email: Email,
  },

  conditions: string[],

  locations: StudyLocation[],
  questions: StudyQuestion[],
  resources: StudyResource[],

  createdAt: Timestamp,
  updatedAt: Timestamp,
}

```

| Name                         | Type              | Default           | Immutable | Notes                                                   |
|------------------------------|-------------------|-------------------|-----------|---------------------------------------------------------|
| `activated`                  | `boolean`         | `true`            | false     | whether study is shown to participants or not           |
| `title`                      | `string`          | *set at creation* | false     | must be between 50 and 100 characters                   |
| `description`                | `string`          | *set at creation* | false     | must be between 300 and 500 characters                  |
| `sex`                        | `StudySex`        | *set at creation* | false     | -                                                       |
| `minAge`                     | `number`          | *set at creation* | false     | must be between 0 and `maxAge`                          |
| `maxAge`                     | `number`          | *set at creation* | false     | must be between `minAge` and 100                        |
| `acceptsHealthyParticipants` | `boolean`         | *set at creation* | false     | -                                                       |
| `acceptsRemoteParticipants`  | `boolean`         | *set at creation* | false     | -                                                       |
| `type`                       | `StudyType`       | *set at creation* | false     | -                                                       |
| `researcher.id`              | `UserID`          | *set at creation* | true      | uid of researcher who created study (user.uid)          |
| `researcher.name`            | `string`          | *set at creation* | true      | name of researcher who created study (user.displayName) |
| `researcher.email`           | `Email`           | *set at creation* | true      | email of researcher who created study (user.email)      |
| `conditions`                 | `string[]`        | *set at creation* | false     | -                                                       |
| `locations`                  | `StudyLocation[]` | *set at creation* | false     | -                                                       |
| `questions`                  | `StudyQuestion[]` | *set at creation* | false     | -                                                       |
| `resources`                  | `StudyResource[]` | *set at creation* | false     | -                                                       |
| `createdAt`                  | `Timestamp`       | *set at creation* | true      | -                                                       |
| `updatedAt`                  | `Timestamp`       | *set on update*   | false     | -                                                       |

---

## Study Participant Document

```ts
// CUSTOM TYPES

type StudyParticipantStatus = "interested" | "consented" |  "screened" | "accepted" | "rejected"

type StudyParticipantResponse = "Yes" | "No" | "Unsure"

```

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}

{
  questions: StudyQuestion[],
  responses: StudyParticipantResponse[]
  status: StudyParticipantStatus,
  fakename: string,
  timezone: Timezone,
  availability: string,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}

```

| Name           | Type                         | Default           | Immutable | Notes                                                                          |
|----------------|------------------------------|-------------------|-----------|--------------------------------------------------------------------------------|
| `questions`    | `StudyQuestion[]`            | *set at creation* | true      | must be the same length as the list of questions in study `studyID`            |
| `responses`    | `StudyParticipantResponse[]` | *set at creation* | true      | must be the same length as the list of questions in study `studyID`            |
| `status`       | `StudyParticipantStatus`     | `"interested"`    | false     | -                                                                              |
| `fakename`     | `string`                     | *set at creation* | true      | -                                                                              |
| `timezone`     | `Timezone`                   | *set at creation* | true      | copied from participant document (valid US timezone from moment-timezone list) |
| `availability` | `string`                     | *set at creation* | true      | copied from participant document (must be between 0 and 500 characters)        |
| `createdAt`    | `Timestamp`                  | *set at creation* | true      | -                                                                              |
| `updatedAt`    | `Timestamp`                  | *set on update*   | false     | -                                                                              |

**Notes:**

* `participantID` is the enrolled participant's firebase uid
* Document can only be created by participant
* Document can only be updated by researcher
* The fields timezone and availability are copied from the participant's document on creation

* [MAINTENANCE] When participant changes personal timezone, update `timezone`
* [MAINTENANCE] When participant changes personal availability, update `availability`
* [MAINTENANCE] When participant deletes account, delete document

---

## Note Document

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}/notes/{noteID}

{
  title: string,
  body: string,
  participantID: UserID,
  researcherID: UserID,
  studyID: DocumentID,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}
```

| Name            | Type         | Default           | Immutable | Notes                                                   |
|-----------------|--------------|-------------------|-----------|---------------------------------------------------------|
| `title`         | `string`     | *set at creation* | false     | must be between 1 and 100 characters                    |
| `body`          | `string`     | *set at creation* | false     | must be between 1 and 500 characters                    |
| `participantID` | `UserID`     | *set at creation* | true      | uid of participant who enrolled in the study            |
| `researcherID`  | `UserID`     | *set at creation* | true      | uid of researcher who created the study the note is for |
| `studyID`       | `DocumentID` | *set at creation* | true      | `studyID` of the study the note is for                  |
| `createdAt`     | `Timestamp`  | *set at creation* | true      | -                                                       |
| `updatedAt`     | `Timestamp`  | *set on update*   | false     | -                                                       |

---

## Message Document

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}/messages/{messageID}

{
  text: string,
  read: boolean,
  sender: UserID,
  researcherID: UserID,
  participantID: UserID,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}
```

| Name        | Type        | Default           | Immutable | Notes                                                                        |
|-------------|-------------|-------------------|-----------|------------------------------------------------------------------------------|
| `text`      | `string`    | *set at creation* | true      | contents of the message                                                      |
| `read`      | `boolean`   | `false`           | false     | can only be changed from `false` to `true` by other user in the conversation |
| `sender`      | `UserID`    | *set at creation* | true      | uid of user who sent the message                                             |
| `researcherID`      | `UserID`    | *set at creation* | true      | uid of researcher who is part of conversation                                            |
| `participantID`      | `UserID`    | *set at creation* | true      | uid of participant who is part of conversation                                             |
| `createdAt` | `Timestamp` | *set at creation* | true      | time at which message was sent                                               |
| `updatedAt` | `Timestamp` | *set on update*   | false     | time at which message was read                                               |

**Notes:**

* Document can be created by either the researcher or participant (request.auth.uid == study.researcher.id || request.auth.uid == participantID)
* Document can be updated only by the user that didn't create the document by changing read from `false` to `true` (request.auth.uid != user)
* If the researcher creates the document, the value of user must be set to researcherID (auth.currentUser.uid)
* If the participant creates the document, the value of user must be set to participantID (auth.currentUser.uid)

---

## Meeting Document

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}/meetings/{meetingID}

{
  name: string,
  link: URL,
  time: Timestamp,
  confirmedByParticipant: boolean,
  participantID: UserID,
  researcherID: UserID,
  studyID: DocumentID,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}
```

| Name                     | Type         | Default           | Immutable | Notes                                                                                  |
|--------------------------|--------------|-------------------|-----------|----------------------------------------------------------------------------------------|
| `name`                   | `string`     | *set at creation* | false     | -                                                                                      |
| `link`                   | `URL`        | *set at creation* | false     | online meeting link (zoom/meet)                                                        |
| `time`                   | `Timestamp`  | *set at creation* | false     | time at which the meeting is scheduled for                                             |
| `confirmedByParticipant` | `boolean`    | `false`           | false     | has the participant confirmed the meeting (can only be changed from `false` to `true`) |
| `participantID`          | `UserID`     | *set at creation* | true      | uid of participant who enrolled in the study                                           |
| `researcherID`           | `UserID`     | *set at creation* | true      | uid of researcher who created the study the meeting is for                             |
| `studyID`                | `DocumentID` | *set at creation* | true      | `studyID` of the study the meeting is for                                              |
| `createdAt`              | `Timestamp`  | *set at creation* | true      | -                                                                                      |
| `updatedAt`              | `Timestamp`  | *set on update*   | false     | -                                                                                      |

**Notes:**

* Document can only be created by the researcher
* Researcher can only update name, link, and time
* Participant can only update confirmedByParticipant from `false` to `true`
* Participant with `participantID` must be enrolled in study with `studyID` (/studies/{studyID}/participants/{participantID} must exist)
* Researcher with `researcherID` must have ownership of study with `studyID` (study.researcher.id must be the same as researcherID)

---

## Reminder Document

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}/reminders/{reminderID}

{
  title: string,
  times: WeeklyOffset[],
  startDate: Date,
  endDate: Date,
  confirmedByParticipant: boolean,
  participantID: UserID,
  researcherID: UserID,
  studyID: DocumentID,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}
```

| Name                     | Type             | Default           | Immutable | Notes                                                                                   |
|--------------------------|------------------|-------------------|-----------|-----------------------------------------------------------------------------------------|
| `title`                  | `string`         | *set at creation* | false     | -                                                                                       |
| `times`                  | `WeeklyOffset[]` | *set at creation* | false     | list of weekly offsets at which reminder is sent                                        |
| `startDate`              | `Date`           | *set at creation* | false     | must be in future                                                                       |
| `endDate`                | `Date`           | *set at creation* | false     | must be after `startDate`                                                               |
| `confirmedByParticipant` | `boolean`        | `false`           | false     | has the participant confirmed the reminder (can only be changed from `false` to `true`) |
| `participantID`          | `UserID`         | *set at creation* | true      | uid of participant who enrolled in the study                                            |
| `researcherID`           | `UserID`         | *set at creation* | true      | uid of researcher who created the study the reminder is for                             |
| `studyID`                | `DocumentID`     | *set at creation* | true      | `studyID` of the study the reminder is for                                              |
| `createdAt`              | `Timestamp`      | *set at creation* | true      | -                                                                                       |
| `updatedAt`              | `Timestamp`      | *set on update*   | false     | -                                                                                       |

**Notes:**

* Document can only be created by the researcher
* Researcher can only update title, times, startDate, and endDate
* Participant can only update confirmedByParticipant from `false` to `true`
* Document can be updated only by the user that didn't create the document by changing read from `false` to `true` (request.auth.uid != user)
* Participant with `participantID` must be enrolled in study with `studyID` (/studies/{studyID}/participants/{participantID} must exist)
* Researcher with `researcherID` must have ownership of study with `studyID` (study.researcher.id must be the same as researcherID)

---

## Mailing Document

```ts
// DOCUMENT PATH: /mailing/{mailingID}

{
  side: Side,
  email: Email,
  createdAt: Timestamp,
  updatedAt: Timestamp,
}
```

| Name        | Type        | Default           | Immutable | Notes                                                                               |
|-------------|-------------|-------------------|-----------|-------------------------------------------------------------------------------------|
| `side`      | `Side`  | *set at creation* | false     | which website side (researcher/participant) did the user join the mailing list from |
| `email`     | `Email`     | *set at creation* | false     | -                                                                                   |
| `createdAt` | `Timestamp` | *set at creation* | true      | time at which email was submitted                                                   |
| `updatedAt` | `Timestamp` | *set on creation* | true      | redundant for now as feedback is never updated                                      |


**Notes:**

* Only create option allowed as this data is used internally

---

## Feature Document

* Only create mutation allowed as this data is used internally

```ts
// CUSTOM TYPES

type FeedbackSystem = "Android" | "iOS" | "macOS" | "Windows" | "Linux" | "Other";

type FeedbackBroswer = "Firefox" | "Opera" | "Internet Edge" | "Chrome" | "Safari" | "Other";

```

```ts
// DOCUMENT PATH: /features/{featureID}

{
  side: Side;
  name: string;
  email: Email;
  description: string;
  createdAt: Timestamp;
  updatedAt: Timestamp;
}
```

| Name        | Type              | Default           | Immutable | Notes                                                                  |
|-------------|-------------------|-------------------|-----------|------------------------------------------------------------------------|
| `side`      | `Side`        | *set at creation* | true      | which website side (researcher/participant) was the feedback sent from |
| `name`     | `string`          | *set at creation* | true      | between 1 and 100 characters                                           |
| `description`      | `string`          | *set at creation* | true      | between 1 and 500 characters                                           |
| `email`     | `Email`           | *set at creation* | true      | must be the same as the authenticated user's email                     |
| `createdAt` | `Timestamp`       | *set at creation* | true      | time at which feedback was submitted                                   |
| `updatedAt` | `Timestamp`       | *set on creation* | true      | redundant for now as feedback is never updated                         |


**Notes:**

* Only create mutation allowed as this data is used internally

---

## Bug Document

* Only create mutation allowed as this data is used internally

```ts
// CUSTOM TYPES

type BugSystem = "Android" | "iOS" | "macOS" | "Windows" | "Linux" | "Other";

type BugBrowser = "Firefox" | "Opera" | "Internet Edge" | "Chrome" | "Safari" | "Other";

```

```ts
// DOCUMENT PATH: /bugs/{bugID}

{
  side: Side;
  email: Email;
  system: BugSystem;
  browser: BugBrowser;
  description: string;
  createdAt: Timestamp;
  updatedAt: Timestamp;
}
```

| Name        | Type              | Default           | Immutable | Notes                                                                  |
|-------------|-------------------|-------------------|-----------|------------------------------------------------------------------------|
| `side`     | `Side`          | *set at creation* | true      | which website side (researcher/participant) was the feedback reported                                           |
| `email`      | `Email`          | *set at creation* | true      | must be the same as the authenticated user's email                                            |
| `system`      | `BugSystem`        | *set at creation* | true      | system used by the user |
| `browser`     | `BugBrowser`           | *set at creation* | true      | browser used by the user                     |
| `description`    | `string`  | *set at creation* | true      |    between 1 and 500 characters                                            |
| `createdAt` | `Timestamp`       | *set at creation* | true      | time at which bug was reported                                   |
| `updatedAt` | `Timestamp`       | *set on creation* | true      | redundant for now as feedback is never updated                         |


**Notes:**

* Only create mutation allowed as this data is used internally
