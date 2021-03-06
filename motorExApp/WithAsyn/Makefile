#FILENAME...     Makefile
#USAGE...        Makefile for motor application example with Asyn


# "#!" marks lines that can be uncommented.

TOP = ../..
include $(TOP)/configure/CONFIG

PROD_IOC_DEFAULT = WithAsyn
PROD_IOC_vxWorks = WithAsynVx

COMMONDBDS  = base.dbd
COMMONDBDS += motorSupport.dbd
COMMONDBDS += devSoftMotor.dbd
COMMONDBDS += motorSimSupport.dbd
COMMONDBDS += asyn.dbd
COMMONDBDS += drvAsynSerialPort.dbd
COMMONDBDS += drvAsynIPPort.dbd
ifdef BUSY
	COMMONDBDS += busySupport.dbd
	COMMONLIBS := busy $(COMMONLIBS)
endif

DBD += WithAsyn.dbd
WithAsyn_DBD += $(COMMONDBDS)
ifdef SNCSEQ
	# seq-2-1 and earlier has devSequencer
	ifeq (seq-2-1, $(findstring seq-2-1, $(SNCSEQ)))
		WithAsyn_DBD += devSequencer.dbd
	else ifeq (seq-2.1, $(findstring seq-2.1, $(SNCSEQ)))
		WithAsyn_DBD += devSequencer.dbd
	endif

endif

DBD += WithAsynVx.dbd
WithAsynVx_DBD += $(COMMONDBDS)
#!WithAsynVx_DBD += drvGsIP488.dbd
ifdef IPAC
WithAsynVx_DBD += MiscVx.dbd
endif

WithAsyn_SRCS   += WithAsyn_registerRecordDeviceDriver.cpp
WithAsyn_SRCS_DEFAULT += WithAsynMain.cpp
WithAsynVx_SRCS += WithAsynVx_registerRecordDeviceDriver.cpp

WithAsyn_OBJS_vxWorks += $(EPICS_BASE_BIN)/vxComLibrary

COMMONLIBS += softMotor
COMMONLIBS += motorSimSupport
COMMONLIBS += motor

# Needed for SNL programs
WithAsyn_LIBS += $(COMMONLIBS)
WithAsyn_LIBS += asyn
ifdef SNCSEQ
	# seq-2-1 and earlier has devSequencer
	ifeq (seq-2-1, $(findstring seq-2-1, $(SNCSEQ)))
		WithAsyn_LIBS += seqDev seq pv
	else ifeq (seq-2.1, $(findstring seq-2.1, $(SNCSEQ)))
		WithAsyn_LIBS += seqDev seq pv
	else
		# seq 2.2.
		WithAsyn_LIBS += seq pv
	endif
endif
WithAsyn_LIBS += $(EPICS_BASE_IOC_LIBS)

WithAsynVx_LIBS += $(COMMONLIBS)
ifdef IPAC
WithAsynVx_LIBS += Ipac TyGSOctal
endif
WithAsynVx_LIBS += asyn
# Needed for SNL programs
ifdef SNCSEQ
	ifeq (seq-2-1, $(findstring seq-2-1, $(SNCSEQ)))
		WithAsynVx_LIBS += seqDev seq pv
	else ifeq (seq-2.1, $(findstring seq-2.1, $(SNCSEQ)))
		WithAsynVx_LIBS += seqDev seq pv
	else
		# seq 2.2.
		WithAsynVx_LIBS += seq pv
	endif
endif
WithAsynVx_LIBS += $(EPICS_BASE_IOC_LIBS)

include $(TOP)/configure/RULES

