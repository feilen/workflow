# Workflow

This is a simple document repo for cataloguing how I've streamlined everything from coding to health, so you don't have to! Much of this will be documenting one-off things I made primarily for myself, as opposed to wider codebase contributions I've been able to give back.

A unifying factor here is that, anything and everything that can be automated will be, even at great effort, as Automatic Feilen always puts in the same effort where Regular Feilen can't.

## Code

### dotfiles

I put a little work into making my [dotfiles](https://github.com/feilen/dotfiles) repo 'deployable', so as long as prerequisites are installed on a new computer, it only takes me a minute or two to drop-in my configuration and have my familiar development environment going... even if I'm on termux on a phone, or WSL... etc. Consistency is the major advantage to sticking to a too-configured Vim these days.

### Jumping into a new codebase

Not an original idea, but peppering fuzzy searching and Ripgrep throughout your workflow is incredibly powerful. I've customized my Vim/Tmux to have a very similar setup wherever I am - Ctrl + G (to ripgrep) or Ctrl + F (to filesearch) anywhere, and then wherever possible, preview the highlighted file/line. This is trickier if you're on a non-controlled development server as many of the legacy plugins I use with Vim don't backport that far, so I've ended up making a few modifications to autoload only working versions.

## Home

### Keeping stock

I use a huge number of subscription services to keep household essentials stocked, but it's reasonably easy to keep track of. Not to name any in particular, but household products can generally be subscribed to in bulk for cheaper than average (for my area) but food items end up being more expensive but picky - on average it about evens out, and keeps it off of my mind.

The only by-name subscription I'd point out is Counterculture Coffee's 'slow motion' coffee - it's _extremely good_ decaf coffee, which has put a sizable dent in my caffeine habit. Also good for a sugarfree desert replacement whenever the mood hits.

### Home automation

I use [openhab](openhab.org/) for my home automation, as well as Hue lights/bridge, WeMo smart plugs, and a local server. Any device which phones home is as isolated from the home network as possible, and while on the wifi is only allowed to talk to the server.

The most 'day to day' use I get out of this is maximizing artificial sunlight - I wrote a simple algorithm to approxiate the sun's color temperature based on current time of day, sunrise and sunset, and this is applied to all lights periodically. Any lights in odd or hard to reach places turn on automatically in the morning (kitchen, hallway) where ordinarily there's enough light to see but it's somewhat gloomy. The algorithm in question is pretty primitive:

```
var calculateColorTemp = [ DateTime time, DateTime sunrise, DateTime sunset |                                                                                                 // This is for Hue Ambiance & Color, White Ambiance is a slightly different range.                                                                                           var colorTempToRange = [ Number colortemp |                                                                                                                                   var Number calculated = 100.0 - ((colortemp.doubleValue() - 2200) / 44)                                                                                                     calculated.doubleValue()                                                                                                                                                   ]                                                                                                                                                                           // Start with minimum color                                                                                                                                                 var Number calculatedColor = colorTempToRange.apply(ColortempMin.state)                                                                                                     // if before or after sunset, always evaluate to base color                                                                                                                 if((time.getMillis() > sunrise.getMillis()) && (time.getMillis()) < sunset.getMillis()) {
    var solarDayLength = sunset.getMillis() - sunrise.getMillis()                                                                                                               // -----var colorFloor = Math::cos((solarDayLength.doubleValue() * Math::PI) / 86400000)                                                                                     var timeInDay = time.getMillis() - sunrise.getMillis() - (solarDayLength/2)                                                                                                 // From -1.0 to 1.0                                                                                                                                                         var currentDayX = (timeInDay.doubleValue()) / (solarDayLength.doubleValue()/2)                                                                                               // Algorithm: -sqrt(1-x^2) * (colortempSunset - colortempNoon) + colortempSunset from -1 to 1                                                                               calculatedColor = Math::min(colorTempToRange.apply(ColortempSunset.state) - Math::sqrt(1.0 - Math::pow(currentDayX, 2)) * (colorTempToRange.apply(ColortempSunset.state) - colorTempToRange.apply(ColortempNoon.state)), colorTempToRange.apply(ColortempMin.state)) 
    logInfo("lighting.rules", "Calculated color for {} (rise {}, set {}): {}", time, sunrise, sunset, calculatedColor)
  }                                                                                                                                                                           // no return... awkward                                                                                                                                                     calculatedColor.intValue
]
```

Aside from that, it's super useful for things like turning on cozy star lights instead of the overhead lights in the bedroom if it's after 10, turning dimming lights by default in the evening, or switching on the bedroom fan at night for white noise.

## Health

### Sleep

TODO: Timelimit

### Fitness

TODO: Timelimit additions

### Entertainment

TODO: Art script

## Planning

### Calendar

TODO: Sync, caldavsync and the other one

### Tasks

TODO: tasks.org

## Misc

### Phone

TODO: KISS + additions

TODO: Tasker and friends
