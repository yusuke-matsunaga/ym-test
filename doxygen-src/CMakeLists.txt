
# ===================================================================
# インクルードパスの設定
# ===================================================================


# ===================================================================
#  マクロの定義
# ===================================================================


# ===================================================================
# サブディレクトリの設定
# ===================================================================


# ===================================================================
#  ソースファイルの設定
# ===================================================================


# ===================================================================
#  library ターゲットの設定
# ===================================================================


# ===================================================================
# doxygen 起動用のコマンド
# ===================================================================

# doxygen の対象となるヘッダファイル(のパタン)を YM_DOXY_SRCS に入れる．
set ( YM_DOXY_SRCS )
foreach ( dir
    "${CMAKE_CURRENT_SOURCE_DIR}"
    "${PROJECT_SOURCE_DIR}/ym-base/include"
    "${PROJECT_SOURCE_DIR}/ym-bnet/include"
    "${PROJECT_SOURCE_DIR}/ym-cell/include"
    "${PROJECT_SOURCE_DIR}/ym-combopt/include"
    "${PROJECT_SOURCE_DIR}/ym-common/include"
    "${PROJECT_SOURCE_DIR}/ym-logic/include"
    "${PROJECT_SOURCE_DIR}/ym-mvn/include"
    "${PROJECT_SOURCE_DIR}/ym-sat/include"
    "${PROJECT_SOURCE_DIR}/ym-verilog/include"
    )
  list ( APPEND YM_DOXY_SRCS ${dir} )
endforeach()

# YM_DOXY_SRCS を Doxyfile の INPUT 用に変換する．
string ( REPLACE ";" " " YM_DOXY_INPUT "${YM_DOXY_SRCS}" )

# Doxyfile の生成
configure_file (
  "${CMAKE_CURRENT_SOURCE_DIR}/Doxyfile.in"
  "Doxyfile"
  )

# doxygen 用ターゲット
add_custom_target(dox ALL
  DEPENDS "${CMAKE_CURRENT_BINARY_DIR}/docs/html/index.html"
  )

# doxygen 起動ルール
add_custom_command(
  COMMAND "${DOXYGEN_EXECUTABLE}" ">" "doxygen.log"
  DEPENDS "${CMAKE_CURRENT_BINARY_DIR}/Doxyfile" ${YM_DOXY_SRCS}
  OUTPUT "${CMAKE_CURRENT_BINARY_DIR}/docs/html/index.html"
  COMMENT "generating doxygen documents"
  )

# 生成物のインストールルール
install (DIRECTORY
  "${CMAKE_CURRENT_BINARY_DIR}/docs"
  DESTINATION share/ym-test/
  )
