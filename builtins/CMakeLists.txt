include_directories(../msg)
include_directories(../basecode)
include_directories(../external/muparser)
add_library(moose_builtins
    Arith.cpp
    Group.cpp
    Mstring.cpp
    Func.cpp
    TableBase.cpp
    Table.cpp
    TimeTable.cpp
    Stats.cpp
    Interpol2D.cpp
    HDF5WriterBase.cpp
    StimulusTable.cpp
    HDF5DataWriter.cpp
    testBuiltins.cpp
    )
