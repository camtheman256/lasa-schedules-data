# lasa-schedules-data
The repository for the [LASA Schedules 3](https://github.com/camtheman256/lasa-schedules-3) data files.

## Updating the Schedules

Updating the schedules can be done by editing the two JSON files in this repo.

If you'd like to edit the schedules JSON in a graphical format, use [LASA Schedules Editor](https://schedules-editor.lasa2019.com).

GitHub Pages will automatically build and deploy all commits to https://schedules-data.lasa2019.com/, which is where LASA Schedules 3 pulls schedule data from.

### `schedule.json`

`schedule.json` contains an array of each of the schedule forms with the format:

```json
[{
  "name": "Schedule Name",
  "combinedAB": true,
  "dates": ["1/1/19", ["1/2/19", "2/1/19"]],
  "applyDay": [3],
  "schedule": [{
    "name": "Period Name",
    "startTime": "00:00",
    "endTime": "01:00",
    "runTime": "60"
  }]
}]
```

#### Important Fields

`combinedAB`: this field is a boolean that allows you to specify if a schedule contains both A day periods and B day periods in the same period `name`. If set to true and a slash exists in the string, the 1st character will be used for A days, and the 3rd character will be used for B days.

`dates`: This is an array of date strings in any Javascript `Date()` readable form. An array in this array specifies a range of dates that will be used.

`applyDay`: This is a field that allows you to override the Standard schedule (the first one) for specific days of the week. Note that days are 0-indexed, with 0 as Sunday and 6 as Saturday.

`schedule`: an array of period objects.

`startTime` and `endTime`: These times must be in the form `"00:00"` and in 24-hour form. They are converted to 12-hour form dynamically based on preference.

**Note**: Gaps in time between periods are okay; you do not need to create a separate period for passing. This is calculated automatically.

`runTime`: the number of _minutes_ the period runs for.

### `school-year.json`

This JSON file contains solely holidays that there will be no school on and controls the length the schedule will run in the form:

```json
{
  "holidays": ["1/1/19", ["1/2/19", "2/1/19"]],
  "not_before": "1/1/18",
  "not_after": "12/31/19"
}
```

#### Important Fields

`holidays`: an array of date strings or arrays specifying date ranges with date strings of the days inside `not_before` and `not_after` where school is on holiday. Date ranges are inclusive.

`not_before`: the first day of school.

`not_after`: the last day of school.

### Impromptu Schedule Updates

Because of the easy form of the schedule syntax and by specifying dates, the schedule object can easily be updated for impromptu schedules, such as PSAT, culture day, and finals. However, it is recommended these schedules be removed shortly after they are no longer relevant because they will clutter the tabs on the all schedules screen. In any case, don't let that stop you from contributing schedules yourself.

### Contributing and Updating the Schedules Yourself

The easiest way to do this is the way anyone contributes to any open source project: by creating a fork, updating it on your own repository, and then creating a pull request in camtheman256/lasa-schedules-data. You are welcome to do so to update this app for future years or to accommodate for impromptu schedules.
