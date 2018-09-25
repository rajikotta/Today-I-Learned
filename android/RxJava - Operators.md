## RxJava Operators


*Operators in RxJava are nothing but methods needed to manipulate data that is emitted or create observables.*


|Creational|Transforming|Filtering|Utility|Arithmetic|Combining|Conditional &Boolean 
|--|--| --|--|--|--|--|
|create|buffer|debounce|delay|average|combineLatest|all
|defer| map|distinct|do|count|join|amb
|from|flatmap|elementAt|materialize/dematerialize|sum|merge|contains
| interval|switchmap|filter|observeOn|max|concat|defaultIfEmpty
|just|groupby|ignoreElements|subscribeOn|min|zip|sequenceEqual
|range|scan|sample|timeInterval|reduce|switchOnNext|skipUntil
| repeat|| skip|timeOut|||skipWhile
|timer|| skiplast|timeStamp|||takeWhile
|||take|using|||takeUntil
|||takelast||||