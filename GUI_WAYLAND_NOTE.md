# GUI Mode - Wayland/Sway Compatibility

The GUI mode requires a compatibility flag on Wayland-based systems (like Sway) due to Java Swing's limited Wayland support.

## Working Solution:

**For Wayland/Sway users:**
```bash
export _JAVA_AWT_WM_NONREPARENTING=1
java -jar build/libs/calendar-1.0.jar
```

## Alternative Options:

1. **Use interactive mode:**
   ```bash
   java -jar build/libs/calendar-1.0.jar --mode interactive
   ```

2. **Use headless mode with script:**
   ```bash
   java -jar build/libs/calendar-1.0.jar --mode headless res/commands.txt
   ```

## Complete GUI Features:

### Calendar Management
- Month view with navigation (previous/next month, today button)
- Multiple calendar creation with timezone selection
- Calendar editing (name and timezone)
- Calendar switching via dropdown selector
- Default calendar auto-creation in system timezone

### Event Operations
- Create single events on selected dates
- Create recurring event series with weekday selection
- Edit single event properties
- Edit multiple events from a specific point in time
- Edit entire event series
- View events by clicking on dates
- Event count indicators on calendar dates

### Advanced Features
- Copy single events between calendars with timezone conversion
- Copy all events on a specific date to another calendar
- Copy events in date range to another calendar
- Export calendar to CSV format
- Export calendar to iCal format
- Check availability status (busy/available) at specific times

### Visual Indicators
- Selected date highlighted in green
- Today's date highlighted with blue border
- Event count displayed on dates with events
- Status bar showing operation results
- Timezone display for active calendar

The interactive and headless modes provide full calendar functionality through the command line interface if GUI issues persist on Wayland systems.