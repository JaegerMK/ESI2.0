# esi-objects

A library for simple and efficient upserting of inmation objects

## Changes

version | date | description
------- | ---- | -----------
1 | 2018-04-17 | Initial release

## Available functions

### INFO

This is a mandatory function for every ESI library.

### UPSERTOBJECT

Upserts an object with minimal required count of commits.

```lua
local properties =
{
  [".ObjectName"] = "testfolder",
  [".ObjectDescription"] = "testdesc",
  Custom =
  {
    ["customkey"] = "customvalue",
    ["customkey1"] = "customvalue1"
  }
}

local o, changed = O:UPSERTOBJECT({path=inmation.getself():parent():path(), 
    class = "MODEL_CLASS_GENFOLDER", 
    properties = properties})
```

Chart Example:

```lua
local prop = 
{
  [".ObjectName"] = "testchartname",
  [".ObjectDescription"] = "testdesc",
  [".ChartType"] = 2, -- paretochart
  [".ParetoChart.KPIYAxisLabel"] = "Signal Contribution [%]", 
  [".ParetoChart.KPIXAxisLabel"] = "xlabel", 
  [".ParetoChart.KPIBarSettings.KPIBar"] = {h1:path(), h2:path()}, 
  [".ParetoChart.KPIBarSettings.AggregateSelection"] = {40, 40}, 
  [".ParetoChart.KPIBarSettings.KPIBarName"] = {"test1", "test2"}, 
  [".ParetoChart.KPIBarSettings.KPIBarColor"] = {inmation.model.codes.KPIColors.RED, inmation.model.codes.KPIColors.RED}, 
  [".ParetoChart.KPIBarSettings.KPIBarOffset"] = {" ", " "},
  Custom =
  {
    ["customkey"] = "customvalue",
    ["customkey1"] = "customvalue1"
  }
}

local o, changed = O:UPSERTOBJECT
{path="/BASF/Predictive Maintenance Test/EMEA/Ludwigshafen/Technische Gase/NV6300/Machine", 
    class = "MODEL_CLASS_CHART", 
    properties=prop}
```

### EXISTS

Checks existence of an object

```lua
local exists, object = O:EXISTS{path=o:path()}
local exists, object = O:EXISTS{parentpath=o:parent():path(), objectname=o.ObjectName}
```

### GETCUSTOM

Gets a custom property

```lua
local val = O:GETCUSTOM{object=o, key="asd"} --returns nil if custom key does not exist
local vals, nilkeys = O:GETCUSTOM{object=o, key={"asd1", "asd2"}}
if vals[1]~="v1" or vals[2]~="v2"  then --check nilkeys
    error("invalid values: " .. tostring(vals[1]) .. " " .. tostring(vals[2]) .. " " .. tostring(table.concat(nilkeys)))
end
```

### SETCUSTOM

Sets a custom property

```lua
modLib:SETCUSTOM{object = obj, key = "asd", value = "asd",  disallownewkeys = false}
-- key and value always have to be strings!
modLib:SETCUSTOM{object = obj, key = {"asd1", "asd2"}, value = {"v1, v2"}}
```

### SORTCUSTOM

To come...

## Breaking changes

- Not Applicable