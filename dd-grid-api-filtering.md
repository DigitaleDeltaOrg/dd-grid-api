# DD-GRID-API Generic Filtering Mechanism

Some end points of the DD-GRID-API provide the query parameter "filter". This parameter is meant to offer a generic filtering mechanism.  
Currently, only selecting one or more realizations from an ensemble run is formalized. However, systems may offer additional filter options.

The generic syntax for the query parameter _filter_ is:  
_../some-end-point?filter=attribute:comparer:value_  
Multiple filter criteria are separated by a comma.

The the query parameter _filter_ can (and often will) be used in combination with other query parameters.

## Filtering on ensemble member (_realization_)

This is a mandatory filter, that has to be implemented by every system that offers the DD-GRID-API.

Examples:  
_/coverages/ijsselmeer-prediction-2020-12-08/data?filter=realization:eq:16_&quantity=waterlevel
_/coverages/ijsselmeer-prediction-2020-12-08/data?filter=realization:in:1,7,8,9,15_&quantity=tempature
_/coverages/ijsselmeer-pdf-2020-12-08/data?filter=realization:in:minimum,maximum_&x=6.984&y=53.

If no filtering on ensemble member(s) is requested, the data of all ensemble members will be returned. (The ensemble member identifiers will be an extra dimension in the netcdf file.)

## Filtering on analysis time

An optional filter that systems might implement is selection on analysis time, i.e. the time stamp on which a computation was performed

Example:  
_/coverages?filter=analysisstarttime:eq:2020-07-18T00:00:00Z,analysisendtime:eq:2020-07-19T00:00:00Z&quantity=waterlevel_