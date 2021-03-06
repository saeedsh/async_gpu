#/**********************************************************************
#** This program is part of 'MOOSE', the
#** Messaging Object Oriented Simulation Environment.
#**           copyright (C) 2007 Upinder S. Bhalla. and NCBS
#** It is made available under the terms of the
#** GNU Lesser General Public License version 2.1
#** See the file COPYING.LIB for the full notice.
#**********************************************************************/

TARGET = _ksolve.o

OBJ = \
	KinSparseMatrix.o	\
	ZombiePool.o \
	ZombieBufPool.o \
	ZombieFuncPool.o \
	ZombieReac.o \
	ZombieEnz.o \
	ZombieMMenz.o \
	VoxelPoolsBase.o \
	VoxelPools.o \
	GssaVoxelPools.o \
	RateTerm.o \
	Stoich.o \
	Ksolve.o \
	SteadyState.o \
	Gsolve.o \
	testKsolve.o \

HEADERS = \
	../basecode/header.h \
	../basecode/SparseMatrix.h \
	../basecode/ElementValueFinfo.h \
	RateTerm.h \
	KinSparseMatrix.h \
	ZombiePoolInterface.h \
	Stoich.h \
	../kinetics/Pool.h \
	../kinetics/lookupVolumeFromMesh.h \


# The GSL library (GNU Scientific Library) provides a range of
# numerical functions, which allow us to use various advanced integration
# methods. The GslIntegrator accesses these. This library is licenced
# under the GPL, so only GPL-compliant uses of MOOSE will be able to
# use it. Should be fine for academic use.
# Optional: Comment out the following three items if not using GSL
ifeq ($(USE_GSL),1)
GSL_OBJ = \


GSL_LIBS = -L/usr/lib -lgsl -lgslcblas
GSL_FLAGS = -DUSE_GSL
endif

default: $(TARGET)

$(OBJ)	: $(HEADERS)
KinSparseMatrix.o:	KinSparseMatrix.h ../basecode/SparseMatrix.h
ZombiePool.o:	../kinetics/PoolBase.h ZombiePoolInterface.h ZombiePool.h ../kinetics/lookupVolumeFromMesh.h
ZombieBufPool.o:	../kinetics/PoolBase.h ZombiePoolInterface.h ZombiePool.h ZombieBufPool.h ../kinetics/lookupVolumeFromMesh.h
ZombieBufPool.o:	../kinetics/PoolBase.h ZombiePoolInterface.h ZombiePool.h ZombieFuncPool.h
VoxelPoolsBase.o:	VoxelPoolsBase.h
VoxelPools.o:	VoxelPoolsBase.h VoxelPools.h OdeSystem.h RateTerm.h Stoich.h
GssaVoxelPools.o:	VoxelPoolsBase.h GssaVoxelPools.h ../basecode/SparseMatrix.h KinSparseMatrix.h GssaSystem.h RateTerm.h Stoich.h
RateTerm.o:		RateTerm.h
Stoich.o:		RateTerm.h ../kinetics/FuncTerm.h ../kinetics/SumTotalTerm.h Stoich.h ../kinetics/PoolBase.h ../kinetics/ReacBase.h ../kinetics/EnzBase.h ../kinetics/CplxEnzBase.h ../kinetics/FuncBase.h ../basecode/SparseMatrix.h KinSparseMatrix.h
ZombieReac.o:		RateTerm.h ../kinetics/FuncTerm.h Stoich.h ../kinetics/ReacBase.h ../kinetics/lookupVolumeFromMesh.h ../basecode/SparseMatrix.h KinSparseMatrix.h ZombieReac.h
ZombieEnz.o:		RateTerm.h ../kinetics/FuncTerm.h Stoich.h ../kinetics/EnzBase.h ../kinetics/CplxEnzBase.h ../kinetics/lookupVolumeFromMesh.h ../basecode/SparseMatrix.h KinSparseMatrix.h ZombieEnz.h
ZombieMMenz.o:		RateTerm.h ../kinetics/FuncTerm.h Stoich.h ../kinetics/EnzBase.h ../kinetics/lookupVolumeFromMesh.h ../basecode/SparseMatrix.h KinSparseMatrix.h ZombieMMenz.h
Ksolve.o:		RateTerm.h Stoich.h Ksolve.h VoxelPoolsBase.h VoxelPools.h OdeSystem.h ZombiePoolInterface.h
SteadyState.o:	SteadyState.h ../basecode/SparseMatrix.h KinSparseMatrix.h RateTerm.h ../kinetics/FuncTerm.h Stoich.h ../randnum/randnum.h
Gsolve.o:		RateTerm.h Stoich.h Gsolve.h VoxelPoolsBase.h VoxelPools.h GssaSystem.h ZombiePoolInterface.h ../basecode/SparseMatrix.h KinSparseMatrix.h
testKsolve.o:	../shell/Shell.h

#KineticHub.o:	KineticHub.h

ifeq ($(USE_GSL),1)
#Optional: Comment out the following two items if not using GSL.
$(GSL_OBJ) : $(HEADERS)
#StateScanner.o:	StateScanner.h
endif # !USE_GSL

.cpp.o:
	$(CXX) $(CXXFLAGS) $(GSL_FLAGS) $(SMOLDYN_FLAGS) -I.. -I../basecode -I../msg -I../kinetics -I../mesh $< -c

$(TARGET):		$(OBJ) $(GSL_OBJ) $(SMOLDYN_OBJ) $(HEADERS)
	$(LD) -r -o $(TARGET) $(OBJ) $(GSL_OBJ) $(GSL_LIBS) $(SMOLDYN_OBJ) $(SMOLDYN_LIB_PATH) $(SMOLDYN_LIBS) 

clean:
	-rm -f *.o $(TARGET) core core.*
