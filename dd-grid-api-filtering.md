# DD-GRID-API Generic Filtering Mechanism

Some end points of the DD-GRID-API specify the query parameter "filter". This parameter is meant to offer a generic filtering mechanism. An example of such a filter is: only select one or more realizations from an ensemble run. In addition systems may offer more filter options.  
However, implementing this _filter_ query parameter is optional. Systems may decide to not implement it.

The generic syntax for the query parameter _filter_ is:  
_../some-end-point?filter=attribute:comparer:value_  

The query parameter _filter_ can (and often will) be used in combination with other query parameters.

## Filtering on ensemble member (_realization_)

This is a mandatory filter, that has to be implemented by every system that offers the DD-GRID-API.

Examples:  
/coverages/ijsselmeer-prediction-2020-12-08/data?___filter=realization:eq:16___&quantity=waterlevel  
/coverages/ijsselmeer-prediction-2020-12-08/data?___filter=realization:in:[1,7,8,9,15]___&quantity=tempature  
/coverages/ijsselmeer-pdf-2020-12-08/data?___filter=realization:in:[minimum,maximum]___&x=6.984&y=53.  

If no filtering on ensemble member(s) is requested, the data of all ensemble members will be returned. (The ensemble member identifiers will be an extra dimension in the netcdf file.)

## Filtering on analysis time

An optional filter that systems might implement is selection on analysis time, i.e. the time stamp on which a computation was performed

Example:  
/coverages?___filter=analysisstarttime:eq:2020-07-18T00:00:00Z,analysisendtime:eq:2020-07-19T00:00:00Z___&quantity=waterlevel_
