add_llvm_component_group(MOS)

set(LLVM_TARGET_DEFINITIONS MOS.td)

tablegen(LLVM MOSGenAsmMatcher.inc -gen-asm-matcher)
tablegen(LLVM MOSGenAsmWriter.inc -gen-asm-writer)
tablegen(LLVM MOSGenCallingConv.inc -gen-callingconv)
tablegen(LLVM MOSGenDAGISel.inc -gen-dag-isel)
tablegen(LLVM MOSGenDisassemblerTables.inc -gen-disassembler)
tablegen(LLVM MOSGenGICombiner.inc -gen-global-isel-combiner-matchtable -combiners="MOSCombinerHelper")
tablegen(LLVM MOSGenGlobalISel.inc -gen-global-isel)
tablegen(LLVM MOSGenInstrInfo.inc -gen-instr-info)
tablegen(LLVM MOSGenMCCodeEmitter.inc -gen-emitter)
tablegen(LLVM MOSGenMCPseudoLowering.inc -gen-pseudo-lowering)
tablegen(LLVM MOSGenRegisterBank.inc -gen-register-bank)
tablegen(LLVM MOSGenRegisterInfo.inc -gen-register-info)
tablegen(LLVM MOSGenSearchableTables.inc -gen-searchable-tables)
tablegen(LLVM MOSGenSubtargetInfo.inc -gen-subtarget)

add_public_tablegen_target(MOSCommonTableGen)

add_llvm_target(MOSCodeGen
  MOSAsmPrinter.cpp
  MOSCallLowering.cpp
  MOSCallingConv.cpp
  MOSCombiner.cpp
  MOSCopyOpt.cpp
  MOSInstrCost.cpp
  MOSFrameLowering.cpp
  MOSISelLowering.cpp
  MOSIndexIV.cpp
  MOSInlineAsmLowering.cpp
  MOSIncDecPhi.cpp
  MOSInsertCopies.cpp
  MOSInstrInfo.cpp
  MOSInstructionSelector.cpp
  MOSLateOptimization.cpp
  MOSLegalizerInfo.cpp
  MOSLowerSelect.cpp
  MOSMCInstLower.cpp
  MOSMachineFunctionInfo.cpp
  MOSMachineScheduler.cpp
  MOSNonReentrant.cpp
  MOSPostRAScavenging.cpp
  MOSRegisterBankInfo.cpp
  MOSRegisterInfo.cpp
  MOSShiftRotateChain.cpp
  MOSStaticStackAlloc.cpp
  MOSSubtarget.cpp
  MOSTargetMachine.cpp
  MOSTargetObjectFile.cpp
  MOSZeroPageAlloc.cpp

  DEPENDS
  intrinsics_gen

  LINK_COMPONENTS
  Analysis
  AsmPrinter
  BinaryFormat
  CodeGen
  Core
  GlobalISel
  IPO
  InstCombine
  LTO
  MC
  MOSDesc
  MOSInfo
  Passes
  Scalar
  SelectionDAG
  Support
  Target
  TransformUtils

  ADD_TO_COMPONENT
  MOS
)

add_subdirectory(AsmParser)
add_subdirectory(Disassembler)
add_subdirectory(MCTargetDesc)
add_subdirectory(TargetInfo)
