# Document Paths and Structures

## Researcher Document

```ts
// DOCUMENT PATH: /researchers/{researcherID}

{
    organization: string,
    background: string,
    timezone: {
        region: Timezone,
        autodetect: boolean,
    },
    notifications: {
        local: boolean,
        email: boolean,
        phone: boolean,
    },
}

```

| Name                  | Type       | Default           | Immutable | Notes                                            |
|-----------------------|------------|-------------------|-----------|--------------------------------------------------|
| `organization`        | `string`   | ""                | false     | must be between 0 and 100 characters             |
| `background`          | `string`   | ""                | false     | must be between 0 and 500 characters             |
| `timezone.region`     | `Timezone` | *set at creation* | false     | must be a valid US timezone from moment-timezone |
| `timezone.autodetect` | `boolean`  | `true`            | false     | -                                                |
| `notifications.local` | `boolean`  | `true`            | false     | -                                                |
| `notifications.email` | `boolean`  | `true`            | false     | -                                                |
| `notifications.phone` | `boolean`  | `false`           | false     | -                                                |

---

## Researcher Notification Document

```ts
// CUSTOM TYPES

type ResearcherNotificationCode = "CREATE_ACCOUNT" | "DELETE_ACCOUNT" | "CREATE_STUDY" | "DELETE_STUDY" | "PARTICIPANT_ENROLLED" | "PARTICIPANT_CONFIRMED_MEETING" | "PARTICIPANT_CONFIRMED_REMINDER" | "MEETING_NOW"
```

```ts
// DOCUMENT PATH: /researchers/{researcherID}/notifications/{notificationID}

{
  code: ResearcherNotificationCode,
  time: Timestamp,
  link: URL,
  read: boolean,
  title: string,
  description: string,
}

```

| Name          | Type                         | Default           | Immutable | Notes                                                                                |
|---------------|------------------------------|-------------------|-----------|--------------------------------------------------------------------------------------|
| `code`        | `ResearcherNotificationCode` | *set at creation* | true      | determines notification type, icon, and color                                        |
| `time`        | `Timestamp`                  | *set at creation* | true      | time at which notification was sent                                                  |
| `link`        | `URL`                        | *set at creation* | true      | redirect link to relevant content on notification click                              |
| `title`       | `string`                     | *set at creation* | true      | -                                                                                    |
| `description` | `string`                     | *set at creation* | true      | -                                                                                    |
| `read`        | `boolean`                    | `false`           | false     | has notification  been read by the user (can only be changed from `false` to `true`) |

---

## Participant Document

```ts
// CUSTOM TYPES

type BiologicalSex = "Male" | "Female"
```

```ts
// DOCUMENT PATH: /participants/{participantID}

{
    sex: BiologicalSex,
    birthdate: Date,
    availability: string,
    timezone: {
        region: Timezone,
        autodetect: boolean,
    },
    location: {
        address: Address,
        coordinates: {
            latitude: Latitude,
            longitude: Longitude,
        },
        autodetect: boolean,
    },
    notifications: {
        local: boolean,
        email: boolean,
        phone: boolean,
    },
}

```

| Name                            | Type            | Default           | Immutable | Notes                                            |
|---------------------------------|-----------------|-------------------|-----------|--------------------------------------------------|
| `sex`                           | `BiologicalSex` | `""`              | false     | -                                                |
| `birthdate`                     | `Date`          | `""`              | false     | -                                                |
| `availability`                  | `string`        | `""`              | false     | must be between 0 and 500 characters             |
| `timezone.region`               | `Timezone`      | *set at creation* | false     | must be a valid US timezone from moment-timezone |
| `timezone.autodetect`           | `boolean`       | `true`            | false     | -                                                |
| `location.address`              | `Address`       | *set at creation* | false     | must be a valid address from Google Places API   |
| `location.coordinates.latitude` | `Latitude`      | *set at creation* | false     | -                                                |
| `location.coordinates.latitude` | `Longitude`     | *set at creation* | false     | -                                                |
| `location.autodetect`           | `boolean`       | `true`            | false     | -                                                |
| `notifications.local`           | `boolean`       | `true`            | false     | -                                                |
| `notifications.email`           | `boolean`       | `true`            | false     | -                                                |
| `notifications.phone`           | `boolean`       | `false`           | false     | -                                                |

---

## Participant Notification Document

```ts
// CUSTOM TYPES

type ParticipantNotificationCode = "CREATE_ACCOUNT" | "DELETE_ACCOUNT" | "RESEARCHER_SENT_MESSAGE" | "RESEARCHER_CREATED_MEETING" | "RESEARCHER_UPDATED_MEETING" | "RESEARCHER_DELETED_MEETING" | "RESEARCHER_CREATED_REMINDER" | "RESEARCHER_UPDATED_REMINDER" | "RESEARCHER_DELETED_REMINDER" | "RESEARCHER_CHANGED_PARTICIPANT_STATUS" | "MEETING_NOW" | "REMINDER_NOW"
```

```ts
// DOCUMENT PATH: /researchers/{researcherID}/notifications/{notificationID}

{
  code: ParticipantNotificationCode,
  time: Timestamp,
  link: URL,
  read: boolean,
  title: string,
  description: string,
}

```

| Name          | Type                         | Default           | Immutable | Notes                                                                               |
|---------------|------------------------------|-------------------|-----------|-------------------------------------------------------------------------------------|
| `code`        | `ResearcherNotificationCode` | *set at creation* | true      | determines notification type, icon, and color                                       |
| `time`        | `Timestamp`                  | *set at creation* | true      | time at which notification was sent                                                 |
| `link`        | `URL`                        | *set at creation* | true      | redirect link to relevant content on notification click                             |
| `title`       | `string`                     | *set at creation* | true      | -                                                                                   |
| `description` | `string`                     | *set at creation* | true      | -                                                                                   |
| `read`        | `boolean`                    | `false`           | false     | has notification been read by the user (can only be changed from `false` to `true`) |

---

## Study Document

```ts
// CUSTOM TYPES

type EligibleSex = "All" | "Male" | "Female"

type StudyType = "Observational" | "Interventional"

type Location = {
  address: Address,
  coordinates: {
    latitude: Latitude,
    longitude: Longitude,
  },
}

type StudyQuestionType = "Inclusion" | "Exclusion"

type Question = {
  type: StudyQuestionType,
  prompt: string,
}

type Resource = {
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
  sex: EligibleSex,

  minAge: number,
  maxAge: number,
  acceptsHealthyVolunteers: boolean,
  type: StudyType,

  createdAt: Timestamp,
  updatedAt: Timestamp,

  researcher: {
    id: UID,
    name: string,
    email: Email,
  },

  conditions: string[],

  locations: Location[],
  questions: Question[],
  resources: Resource[],
}

```

| Name                       | Type          | Default           | Immutable | Notes                                                   |
|----------------------------|---------------|-------------------|-----------|---------------------------------------------------------|
| `activated`                | `boolean`     | `true`            | false     | -                                                       |
| `title`                    | `string`      | *set at creation* | false     | must be between 50 and 100 characters                   |
| `description`              | `string`      | *set at creation* | false     | must be between 300 and 500 characters                  |
| `sex`                      | `EligibleSex` | *set at creation* | false     | -                                                       |
| `minAge`                   | `number`      | *set at creation* | false     | must be between 0 and `maxAge`                          |
| `maxAge`                   | `number`      | *set at creation* | false     | must be between `minAge` and 100                        |
| `acceptsHealthyVolunteers` | `boolean`     | *set at creation* | false     | -                                                       |
| `type`                     | `StudyType`   | *set at creation* | false     | -                                                       |
| `createdAt`                | `Timestamp`   | *set at creation* | false     | -                                                       |
| `updatedAt`                | `Timestamp`   | *set at update*   | false     | -                                                       |
| `researcher.id`            | `UID`         | *set at creation* | true      | uid of researcher who created study (user.uid)          |
| `researcher.name`          | `string`      | *set at creation* | true      | name of researcher who created study (user.displayName) |
| `researcher.email`         | `Email`       | *set at creation* | true      | email of researcher who created study (user.email)      |
| `conditions`               | `string[]`    | *set at creation* | false     | -                                                       |
| `locations`                | `Location[]`  | *set at creation* | false     | -                                                       |
| `questions`                | `Question[]`  | *set at creation* | false     | -                                                       |
| `resources`                | `Resource[]`  | *set at creation* | false     | -                                                       |

---

## Study Participant Document

```ts
// CUSTOM TYPES

type Status = "interested" | "consented" |  "screened" | "accepted" | "rejected"

type Reponse = "Yes" | "No" | "Unsure"

```

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}

{
  status: Status,
  responses: Reponse[]
  timezone: Timezone,
  availability: string,
}

```

| Name           | Type        | Default           | Immutable | Notes                                                                          |
|----------------|-------------|-------------------|-----------|--------------------------------------------------------------------------------|
| `status`       | `Status`    | `true`            | false     | -                                                                              |
| `responses`    | `Reponse[]` | *set at creation* | true      | must be the same length as the list of questions in study `studyID`            |
| `timezone`     | `Timezone`  | *set at creation* | true      | copied from participant document (valid US timezone from moment-timezone list) |
| `availability` | `string`    | *set at creation* | true      | copied from participant document (must be between 0 and 500 characters)        |

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
  time: Timestamp,
  title: string,
  body: string,
}
```

| Name    | Type        | Default           | Immutable | Notes                                |
|---------|-------------|-------------------|-----------|--------------------------------------|
| `time`  | `Timestamp` | *set at creation* | true      | time at which note was created       |
| `title` | `string`    | *set at creation* | false     | must be between 1 and 100 characters |
| `body`  | `string`    | *set at creation* | false     | must be between 1 and 500 characters |

---

## Message Document

```ts
// DOCUMENT PATH: /studies/{studyID}/participants/{participantID}/messages/{messageID}

{
  time: Timestamp,
  user: UID,
  text: string,
  read: boolean,
}
```

| Name   | Type        | Default           | Immutable | Notes                                                                        |
|--------|-------------|-------------------|-----------|------------------------------------------------------------------------------|
| `time` | `Timestamp` | *set at creation* | true      | time at which message was sent                                               |
| `user` | `UID`       | *set at creation* | true      | uid of user who sent the message                                             |
| `text` | `string`    | *set at creation* | true      | contents of the message                                                      |
| `read` | `boolean`   | `false`           | false     | can only be changed from `false` to `true` by other user in the conversation |

**Notes:**

* Document can be created by either the researcher or participant (request.auth.uid == study.researcher.id || request.auth.uid == participantID)
* Document can be updated only by the user that didn't create the document by changing read from `false` to `true` (request.auth.uid != user)
* If the researcher creates the document, the value of user must be set to researcherID (auth.currentUser.uid)
* If the participant creates the document, the value of user must be set to participantID (auth.currentUser.uid)

---

## Meeting Document

```ts
// DOCUMENT PATH: /meetings/{meetingID}

{
  name: string,
  link: URL,
  time: Timestamp,
  participantID: UID,
  researcherID: UID,
  studyID: DID,
  confirmedByParticipant: boolean,
}
```

| Name                     | Type        | Default           | Immutable | Notes                                                                                  |
|--------------------------|-------------|-------------------|-----------|----------------------------------------------------------------------------------------|
| `name`                   | `string`    | *set at creation* | false     | -                                                                                      |
| `link`                   | `URL`       | *set at creation* | false     | online meeting link (zoom/meet)                                                        |
| `time`                   | `Timestamp` | *set at creation* | false     | time at which the meeting is scheduled for                                             |
| `participantID`          | `UID`       | *set at creation* | true      | uid of participant who enrolled for the study                                          |
| `researcherID`           | `UID`       | *set at creation* | true      | uid of researcher who created the study the meeting is for                             |
| `studyID`                | `DID`       | *set at creation* | true      | `studyID` of the study the meeting is for                                              |
| `confirmedByParticipant` | `boolean`   | `false`           | false     | has the participant confirmed the meeting (can only be changed from `false` to `true`) |

**Notes:**

* Document can only be created by the researcher
* Researcher can only update name, link, and time
* Participant can only update confirmedByParticipant from `false` to `true`
* Participant with `participantID` must be enrolled in study with `studyID` (/studies/{studyID}/participants/{participantID} must exist)
* Researcher with `researcherID` must have ownership of study with `studyID` (study.researcher.id must be the same as researcherID)

---

## Reminder Document

```ts
// DOCUMENT PATH: /reminders/{reminderID}

{
  title: string,
  times: WeeklyOffset[],
  startDate: Date,
  endDate: Date,
  participantID: UID,
  researcherID: UID,
  studyID: DID,
  confirmedByParticipant: boolean,
}
```

| Name                     | Type        | Default           | Immutable | Notes                                                                                   |
|--------------------------|-------------|-------------------|-----------|-----------------------------------------------------------------------------------------|
| `title`                  | `string`    | *set at creation* | false     | -                                                                                       |
| `times`                  | `URL`       | *set at creation* | false     | list of weekly offsets at which reminder is sent                                        |
| `startDate`              | `Timestamp` | *set at creation* | false     | must be in future                                                                       |
| `endDate`                | `Timestamp` | *set at creation* | false     | must be after `startDate`                                                               |
| `participantID`          | `UID`       | *set at creation* | true      | uid of participant who enrolled for the study                                           |
| `researcherID`           | `UID`       | *set at creation* | true      | uid of researcher who created the study the reminder is for                             |
| `studyID`                | `DID`       | *set at creation* | true      | `studyID` of the study the reminder is for                                              |
| `confirmedByParticipant` | `boolean`   | `false`           | false     | has the participant confirmed the reminder (can only be changed from `false` to `true`) |

**Notes:**

* Document can only be created by the researcher
* Researcher can only update title, times, startDate, and endDate
* Participant can only update confirmedByParticipant from `false` to `true`
* Document can be updated only by the user that didn't create the document by changing read from `false` to `true` (request.auth.uid != user)
* Participant with `participantID` must be enrolled in study with `studyID` (/studies/{studyID}/participants/{participantID} must exist)
* Researcher with `researcherID` must have ownership of study with `studyID` (study.researcher.id must be the same as researcherID)

---

## Feedback Document

```ts
// DOCUMENT PATH: /feedback/{feedbackID}

{
  time: Timestamp,
  side: UserType,
  email: Email,
  title: string,
  body: string,
}
```

| Name    | Type        | Default           | Immutable | Notes                                                                  |
|---------|-------------|-------------------|-----------|------------------------------------------------------------------------|
| `time`  | `Timestamp` | *set at creation* | true      | time at which feedback was submitted                                   |
| `side`  | `UserType`  | *set at creation* | true      | which website side (researcher/participant) was the feedback sent from |
| `email` | `Email`     | *set at creation* | true      | must be the same as the authenticated user's email                     |
| `title` | `string`    | *set at creation* | true      | between 1 and 100 characters                                           |
| `body`  | `string`    | *set at creation* | true      | between 1 and 500 characters                                           |

**Notes:**

* Only create option allowed as this data is used internally

---

## Mailing Document

```ts
// DOCUMENT PATH: /mailing/{mailingID}

{
  time: Timestamp,
  side: UserType,
  email: Email,
}
```

| Name    | Type        | Default           | Immutable | Notes                                                                  |
|---------|-------------|-------------------|-----------|------------------------------------------------------------------------|
| `time`  | `string`    | *set at creation* | false     | time at which email was submitted                                      |
| `side`  | `URL`       | *set at creation* | false     | which website side (researcher/participant) was the feedback sent from |
| `email` | `Timestamp` | *set at creation* | false     | -                                                                      |

**Notes:**

* Only create option allowed as this data is used internally
