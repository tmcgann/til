To get the time between two dates:

```js
function timeBetween(earlier, later) {
    return humanize(getDiffInMilliseconds(earlier, later));
}

function getDiffInMilliseconds(earlier, later) {
    const earlierDate = new Date(earlier);
    const laterDate = new Date(later);
    return (laterDate - earlierDate);
}

function humanize(ms) {
    const duration = getDuration(ms);
    return `${Math.floor(duration.value)} ${duration.units}`;
}

function getDuration(ms) {
    const MS_ONE_MINUTE = 60000;
    const MS_ONE_HOUR = MS_ONE_MINUTE * 60;
    const MS_ONE_DAY = MS_ONE_HOUR * 24;
    
    if (ms < MS_ONE_HOUR) {
        return {
            value: (ms / MS_ONE_MINUTE),
            units: 'minutes',
        };
    }
    if (ms < MS_ONE_DAY) {
        return {
            value: (ms / MS_ONE_HOUR),
            units: 'hours',
        };
    }
    return {
        value: (ms / MS_ONE_DAY),
        units: 'days',
    };
}
```

The same thing using MomentJS:

```js
function timeBetween(earlier, later) {
    return humanize(getDiffInMilliseconds(earlier, later));
}

function getDiffInMilliseconds(earlier, later) {
    const DATE_STRING_FORMAT = 'YYYY/MM/DD HH:mm:ss';
    const earlierDate = moment(earlier, DATE_STRING_FORMAT);
    const laterDate = moment(later, DATE_STRING_FORMAT);
    return laterDate.diff(earlierDate);
}

function humanize(ms) {
    const durationFunctionName = getDurationFunctionName(ms);
    const duration = moment.duration(ms)[durationFunctionName]();
    const units = durationFunctionName.substr(2).toLowerCase();
    return `${Math.floor(duration)} ${units}`;
}

function getDurationFunctionName(ms) {
    const MS_ONE_MINUTE = 60000;
    const MS_ONE_HOUR = MS_ONE_MINUTE * 60;
    const MS_ONE_DAY = MS_ONE_HOUR * 24;
    
    if (ms < MS_ONE_HOUR) {
        return 'asMinutes';
    }
    if (ms < MS_ONE_DAY) {
        return 'asHours';
    }
    return 'asDays';
}
```
