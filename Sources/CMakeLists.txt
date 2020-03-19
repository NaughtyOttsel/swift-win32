add_library(SwiftWin32 SHARED
  Application/Application.swift
  Application/ApplicationDelegate.swift
  Application/ApplicationMain.swift
  UI/Button.swift
  UI/Color.swift
  UI/Control.swift
  UI/EdgeInsets.swift
  UI/Font.swift
  UI/Label.swift
  UI/ProgressView.swift
  UI/Screen.swift
  UI/Slider.swift
  UI/TextField.swift
  UI/TextView.swift
  UI/View.swift
  UI/Window.swift
  UI/WindowClass.swift)
target_sources(SwiftWin32 PRIVATE
  CG/AffineTransform.swift
  CG/Point.swift
  CG/Rect.swift
  CG/Size.swift)
target_sources(SwiftWin32 PRIVATE
  Support/Logging.swift
  Support/Range.swift
  Support/Rect+UIExtensions.swift
  Support/String.swift
  Support/WindowsHandle.swift
  Support/WinSDK+Extensions.swift)
target_compile_options(SwiftWin32 PRIVATE
  "SHELL:-Xcc -DNONAMELESSUNION"
  "SHELL:-Xcc -DCOBJMACROS")
target_link_libraries(SwiftWin32 PUBLIC
  ComCtl32
  Gdi32
  User32)
if(ENABLE_LOGGING)
  target_compile_definitions(SwiftWin32 PRIVATE
    ENABLE_LOGGING)
  if(TARGET SwiftLog::Logging)
    target_link_libraries(SwiftWin32 PUBLIC
      SwiftLog::Logging)
  endif()
endif()
set_target_properties(SwiftWin32 PROPERTIES
  INTERFACE_INCLUDE_DIRECTORIES ${CMAKE_Swift_MODULE_DIRECTORY}
  INTERFACE_LINK_DIRECTORIES $<TARGET_LINKER_FILE_DIR:SwiftWin32>)


swift_install(TARGETS SwiftWin32)