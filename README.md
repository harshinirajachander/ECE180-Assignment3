# ECE-180 Assignment #3
Due: Feb 28, 11:15p (PST)

## Preface

We can all remember the simpler days (last week) when homework assignments involved building one simple class. That was fun, right?  Sadly, very few real-world software problems can be implemented so easily. Therefore, this assignment involves multiples classes that have to work together to accomplish the given task. 

## JobCo Plans to Go PUBLIC!

IPO! WOOT WOOT!  It's very exciting when your cool little startup grows up, and is ready to go public. Sure, lots of early employees stand to make a lot of money on their stock grants. But it's not all fun and games you know. The process of "going public" takes a tremendous amount of work, making sure that all of your internal processes are up to the standards necessary to meet public scrutiny. As it turns out, JobCo has more than a few problems, and you've been placed on the "going public" software team. Good luck!

### Calendrical Computations

"Ok everyone, settle down", Chloe says, smiling softly. "As you've all heard, JobCo is going public...", she begins, then stops abruptly as the room explodes into cheers and shouting. Waiting for nearly a minute, she finally continues, "Ok, ok, before you all rush out and buy yourself a Tesla, we have some work to do." 

## Assignment Details

In this assignment, you are going to build a series of classes that support calendrical computations. Dates, times, timezones, and intervals. Customer of your solution will use your classes to do things like creating timers in their own code, or performing timezone conversions within their application. 

At a minimum, you will implement five classes:

```
class Date;
class Time;
class DateTime;
class Timezone;
class Interval;
```

Note that you are free to create any other classes you need in order to support your solution. Presumably, if you add other classes it is to provide functionality to your solution that you have deemed "worthy" to be part of your solution. Totally up to you. Our testing framework will only interact with the five classes we have outlined above.

### About Your Classes

You are free to implement your `Date` class any way you see fit. It must, however, fulfill certain requirements:

- You must be able to construct a `Date` class without any arguments, in which case it refers to the current date/time, assuming the default timezone of GMT
- You must be able to construct a `Date` class using 3 integers (int month, int day, int year)
- You must be able to construct a `Date` class using a well-formed string ("Jan 4, 1961")
- You must be able to copy construct a `Date` from another `Date` class, or convert/construct from a `DateTime` class
- You must be able to ask a `Date` class to return the current `Timezone` that it is based upon
- You must be able to change the timezone a `Date` object is using 
- You must provide a conversion operator from your `Date` class to a const char*. 

```
class Date {
             Date();                             //default to today, in GMT timezone
             Date(const char *aDateTimeString);  //must parse the given string  
             Date(int month, int day, int year); //build date from individual parts
             Date(const Date &aCopy);  
             Date(const DateTime &aCopy);

  ... more members here as necessary...

}
```

#### The Time Class 
asdf

```
class Time {
             Time();                             //default to now(HH:MM:SS) 
             Time(const char *aTimeString);      //must parse fro the given string  
             Time(int anHour, int aMinutes, int aSeconds); //build time from individual parts
             Time(const Time &aCopy);  
             Time(const DateTime &aCopy);

  ... more members here as necessary...

}
```

#### The DateTime Class 
You are free to implement your `DateTime` class any way you see fit. It must, however, fulfill certain requirements:

- You must be able to construct a `DateTime` class without any arguments, in which case it refers to the current date/time, assuming the default timezone of GMT
- You must be able to construct a `DateTime` class using 6 integers (int month, int day, int year, int hour, int mins, int seconds)
- You must be able to construct a `DateTime` class using a well-formed string ("Jan 4, 1961 08:00:00 PST") (or basic variations of that)
- You must be able to copy construct a `DateTime` from another `DateTime` class
- You must be able to convert construct a `DateTime` from another `Date` class
- You must be able to construct a `DateTime` from a `Date` AND a `Time` class
- You must be able to ask a `DateTime` class to return the current `Timezone` that it is based upon
- You must be able to change the timezone a `DateTime` object is using 
- You must provide a conversion operator from your `DateTime` class to a const char*. 
```

class DateTime {
  ...constructors...
  
  Timezone&  getTimezone();
  DateTime&  setTimezone(Timezone &aTimezone);

  ... more members here as necessary...

}
```

#### The Timezone Class 

Timezones can be tricky, so we're keeping the requirements to a minimum. The baseline timezone for your solution is "GMT" -- which refers to Greenwich Mean Time, clock time at the Royal Observatory in Greenwich, London. It is the same all year round and is not affected by Summer Time or Daylight Saving Time.

Although there a more than 20 _actual_ timezones, we will only ever ask you to support four, using an abbreviations:

1. GMT (gmt as specified above)
2. EST (US Eastern standard time)
3. CST (US Central standard time)
4. PST (US Pacific standard time)

Your timezone class must support default construction, copy construction, and construction from one of the four abbreviations listed above. We will also ask your Timezone class to provide a const char* conversion operator in case a caller wants to be able to print out the string value of the current timezone.

```
class Timezone {
  ...constructors...
  
  operator const char*();
  
  ...other members as needed...
};
```

#### The Interval Class 
asdf

### The Testing Interface

In our last assignment, we provided you with a specific class interface. In this assignment, the interface is up to you. Instead, we are providing you with a "boilerplate" test-harness that you'll use to test your implementation. Once you turn in your work, Vlad-the-compiler will use your testing harness to perform operations that we can use to grade your work.  

The testing harness looks like this:

```

class SFString {
public:
  
  SFString();
  SFString(const SFString& aString);
  
  SFString&    operator=(const SFString& aString);
  
  operator const char*() const;
  
  char         operator[](int pos) const;

  SFString&    operator+=(const SFString &aString);
  
  bool         operator<(const SFString &aString);
  bool         operator<=(const SFString &aString);
  bool         operator>(const SFString &aString);
  bool         operator>=(const SFString &aString);
  bool         operator==(const SFString &aString);
  bool         operator!=(const SFString &aString);
  
  int          find(const SFString &aString, size_t offset=0);
  
  SFString&    insert(size_t aPos, const SFString &aString);
  SFString&    insert(size_t aPos, const char aChar);    
  SFString&    replace(size_t pos, size_t len, const SFString &aString);   
  SFString&    erase(size_t pos, size_t len);  
};

```
