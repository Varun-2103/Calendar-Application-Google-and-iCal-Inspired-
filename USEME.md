# Calendar Application - Usage Guide

## Overview

This calendar application supports multiple calendars with timezone management, event copying between calendars, and export to both CSV and iCal formats. The application maintains an MVC architecture and can be run in both interactive and headless modes.

## Running the Application

### JAR Execution

```bash
# Build the JAR file
./gradlew jar

# Interactive mode
java -jar build/libs/calendar-1.0.jar --mode interactive

# Headless mode with command file
java -jar build/libs/calendar-1.0.jar --mode headless res/commands.txt

# Show help
java -jar build/libs/calendar-1.0.jar --help
```

### Command Line Arguments

- `--mode interactive`: Run in interactive mode (default)
- `--mode headless <file>`: Execute commands from file
- `--help`: Show usage information

## Calendar Management

### Create a New Calendar
```bash
create calendar --name Work --timezone America/New_York
create calendar --name Personal --timezone Europe/London
create calendar --name School --timezone Asia/Kolkata
```

### Switch Between Calendars
```bash
use calendar --name Work
use calendar --name Personal
```

### Edit Calendar Properties
```bash
# Change calendar name
edit calendar --name Work --property name "Office"

# Change calendar timezone
edit calendar --name Personal --property timezone America/Los_Angeles
```

## Event Management

### Create Single Events
```bash
# Event with specific time range
create event "Team Meeting" from 2025-12-01T10:00 to 2025-12-01T11:00

# All-day event
create event "Holiday" on 2025-12-25

# Event with quotes in name
create event "Doctor Appointment" from 2025-12-02T14:00 to 2025-12-02T15:00
```

### Create Recurring Events
```bash
# Daily events
create event "Daily Standup" from 2025-12-01T09:00 to 2025-12-01T09:15 repeats daily for 5 times

# Weekly events (specific weekdays)
create event "Team Sync" from 2025-12-01T15:00 to 2025-12-01T15:30 repeats MWF for 4 times

# Weekend events
create event "Weekend Project" from 2025-12-06T10:00 to 2025-12-06T12:00 repeats SS for 3 times
```

## Event Copying

### Copy Single Event
```bash
# Copy specific event to another calendar with timezone conversion
copy event "Team Meeting" on 2025-12-01T10:00 --target Personal to 2025-12-02T10:00
```

### Copy All Events on a Date
```bash
# Copy all events from one day to another calendar
copy events on 2025-12-01 --target Personal to 2025-12-03
```

### Copy Events in Date Range
```bash
# Copy events from a date range to another calendar
copy events between 2025-12-01 and 2025-12-07 --target School to 2025-01-15
```

**Note**: Copy operations automatically convert times between source and target calendar timezones.

## Querying Events

### Print Events
```bash
# Show all events on a specific date
print events on 2025-12-01

# Show events between dates
print events between 2025-12-01 and 2025-12-07
```

### Check Availability
```bash
# Check if busy at specific time
show status on 2025-12-01T10:00
```

## Exporting Calendars

### CSV Export
```bash
export cal /tmp/work_calendar.csv
export cal /home/user/personal.csv
```

### iCal Export (Google Calendar Compatible)
```bash
export cal /tmp/personal_calendar.ical
export cal /home/user/schedule.ical
```

**Note**: Export format is automatically detected by file extension (.csv or .ical).

## Timezone Support

The application supports IANA timezone database format. Examples:
- `America/New_York`
- `Europe/London`
- `Asia/Kolkata`
- `Australia/Sydney`
- `Africa/Cairo`
- `America/Los_Angeles`

Each calendar maintains its own timezone, and all events in that calendar are assumed to be in that timezone.

## Error Handling

The application provides clear error messages for:
- Invalid command syntax
- Missing required arguments
- Invalid timezone formats
- Calendar name conflicts
- Event conflicts
- File I/O errors

## Example Workflow

```bash
# 1. Create work calendar
create calendar --name Work --timezone America/New_York

# 2. Set as active calendar
use calendar --name Work

# 3. Add work events
create event "Team Meeting" from 2025-12-01T10:00 to 2025-12-01T11:00
create event "Lunch" on 2025-12-01

# 4. Create personal calendar
create calendar --name Personal --timezone Europe/London

# 5. Copy work event to personal calendar (with timezone conversion)
copy event "Team Meeting" on 2025-12-01T10:00 --target Personal to 2025-12-01T15:00

# 6. Export personal calendar for Google Calendar
use calendar --name Personal
export cal /tmp/personal.ical
```

## File Paths

The application works with both relative and absolute file paths. When running from the project root, you can use:
- Relative paths: `res/commands.txt`, `export cal calendar.csv`
- Absolute paths: `/home/user/calendar.csv`, `C:\Users\Name\calendar.ical`

## Testing

Example command files are provided in the `res/` directory:
- `commands.txt`: Valid command examples
- `invalid.txt`: Error handling examples

Run these files to test functionality:
```bash
java -jar build/libs/calendar-1.0.jar --mode headless res/commands.txt
java -jar build/libs/calendar-1.0.jar --mode headless res/invalid.txt
```