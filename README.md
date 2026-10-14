# Booking System – individual coding exam

This is a starter project for the individual practical coding exam. The
application targets .NET 10 and contains a console application and xUnit tests.

## Requirements

- .NET 10 SDK

## Run the application

```bash
dotnet run --project src/BookingSystem
```

## Run the tests

```bash
dotnet test
```

Read the separate assignment instructions before starting. The starter project contained intentional defects. Some of these have been fixed, but the application is not yet fully implemented.


## Implemented changes

I have fixed the validation of booking start and end times and corrected the detection of overlapping bookings.

I have also updated the search functionality so that it ignores differences between uppercase and lowercase letters.

The application now filters out cancelled bookings and sorts active bookings by date and start time.

I have documented the debugging process in DEBUGGING.md.

## Test results

I ran the automated tests using Test Explorer in Visual Studio.

12 out of 14 tests passed. The two remaining failing tests concern the cancellation functionality.