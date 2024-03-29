set(LLVM_TARGET_DEFINITIONS ARM.td)

tablegen(ARMGenRegisterInfo.inc -gen-register-info)
tablegen(ARMGenInstrInfo.inc -gen-instr-info)
tablegen(ARMGenCodeEmitter.inc -gen-emitter)
tablegen(ARMGenMCCodeEmitter.inc -gen-emitter -mc-emitter)
tablegen(ARMGenMCPseudoLowering.inc -gen-pseudo-lowering)
tablegen(ARMGenAsmWriter.inc -gen-asm-writer)
tablegen(ARMGenAsmMatcher.inc -gen-asm-matcher)
tablegen(ARMGenDAGISel.inc -gen-dag-isel)
tablegen(ARMGenFastISel.inc -gen-fast-isel)
tablegen(ARMGenCallingConv.inc -gen-callingconv)
tablegen(ARMGenSubtargetInfo.inc -gen-subtarget)
tablegen(ARMGenEDInfo.inc -gen-enhanced-disassembly-info)
tablegen(ARMGenDecoderTables.inc -gen-arm-decoder)

add_llvm_target(ARMCodeGen
  ARMAsmBackend.cpp
  ARMAsmPrinter.cpp
  ARMBaseInstrInfo.cpp
  ARMBaseRegisterInfo.cpp
  ARMCodeEmitter.cpp
  ARMConstantIslandPass.cpp
  ARMConstantPoolValue.cpp
  ARMELFWriterInfo.cpp
  ARMExpandPseudoInsts.cpp
  ARMFastISel.cpp
  ARMFrameLowering.cpp
  ARMGlobalMerge.cpp
  ARMHazardRecognizer.cpp
  ARMISelDAGToDAG.cpp
  ARMISelLowering.cpp
  ARMInstrInfo.cpp
  ARMJITInfo.cpp
  ARMMachObjectWriter.cpp
  ARMMCCodeEmitter.cpp
  ARMMCExpr.cpp
  ARMLoadStoreOptimizer.cpp
  ARMMCInstLower.cpp
  ARMRegisterInfo.cpp
  ARMSelectionDAGInfo.cpp
  ARMSubtarget.cpp
  ARMTargetMachine.cpp
  ARMTargetObjectFile.cpp
  MLxExpansionPass.cpp
  NEONMoveFix.cpp
  Thumb1InstrInfo.cpp
  Thumb1FrameLowering.cpp
  Thumb1RegisterInfo.cpp
  Thumb2ITBlockPass.cpp
  Thumb2InstrInfo.cpp
  Thumb2RegisterInfo.cpp
  Thumb2SizeReduction.cpp
  )

# workaround for hanging compilation on MSVC10
if( MSVC_VERSION EQUAL 1600 )
set_property(
  SOURCE ARMISelLowering.cpp
  PROPERTY COMPILE_FLAGS "/Od"
  )
endif()

add_subdirectory(TargetInfo)
add_subdirectory(AsmParser)
add_subdirectory(Disassembler)
add_subdirectory(InstPrinter)
add_subdirectory(MCTargetDesc)
