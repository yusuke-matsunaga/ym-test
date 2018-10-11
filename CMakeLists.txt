# ===================================================================
# CMAKE のおまじない
# ===================================================================
cmake_minimum_required (VERSION 3.2)

# C++14 の指定
set (CMAKE_CXX_STANDARD 14)


# ===================================================================
# プロジェクト名，バージョンの設定
# ===================================================================

set ( YM_INSTALL_LIBDIR "lib/ym-test" )


# ===================================================================
# オプション
# ===================================================================


# ===================================================================
# パッケージの検査
# ===================================================================
list ( APPEND CMAKE_MODULE_PATH
  "${PROJECT_SOURCE_DIR}/ym-common/cmake"
  )

# doxygen の検査
include( FindDoxygen )

# Python のバージョン指定
set( Python_ADDITIONAL_VERSIONS 3.7 3.6 3.5 3.4 3.3 3.2 3.1 )
include( FindPythonInterp )
include( FindPythonLibs )

# cython の検査
include( UseCython )

# google-perftools の検査
find_package( Gperftools )

# 自前のパッケージをインクルード
include ( YmUtils )

# よく使ういくつかのパッケージの検査を行う．
# このオプションでは popt の検査も行う．
ym_init ( "USE_POPT" )


# ===================================================================
# google-test は内蔵のものを使う．
# ===================================================================
ym_use_gtest ()


# ===================================================================
# CTest モジュールの読み込み
# ===================================================================
include ( CTest )
enable_testing()


# ===================================================================
# ヘッダファイルの生成
# ===================================================================


# ===================================================================
# インクルードパスの設定
# ===================================================================
include_directories(
  ${PROJECT_SOURCE_DIR}/ym-base/include
  ${PROJECT_SOURCE_DIR}/ym-bfo/include
  ${PROJECT_SOURCE_DIR}/ym-bnet/include
  ${PROJECT_SOURCE_DIR}/ym-cell/include
  ${PROJECT_SOURCE_DIR}/ym-common/include
  ${PROJECT_SOURCE_DIR}/ym-fraig/include
  ${PROJECT_SOURCE_DIR}/ym-logic/include
  ${PROJECT_SOURCE_DIR}/ym-mvn/include
  ${PROJECT_SOURCE_DIR}/ym-sat/include
  ${PROJECT_SOURCE_DIR}/ym-verilog/include
  ${PROJECT_SOURCE_DIR}/ym-combopt/include
  ${PROJECT_BINARY_DIR}
  )


# ===================================================================
#  マクロの定義
# ===================================================================


# ===================================================================
# サブディレクトリの設定
# ===================================================================

add_subdirectory( ym-common )
add_subdirectory( ym-base )
add_subdirectory( ym-logic )
add_subdirectory( ym-bfo )
add_subdirectory( ym-sat )
add_subdirectory( ym-cell )
add_subdirectory( ym-bnet )
add_subdirectory( ym-fraig )
add_subdirectory( ym-verilog )
add_subdirectory( ym-mvn)
add_subdirectory( ym-combopt )

add_subdirectory( doxygen-src )


# ===================================================================
#  ソースファイルの設定
# ===================================================================


# ===================================================================
#  library ターゲットの設定


# ===================================================================
# python スクリプト用のインストールターゲット
# ===================================================================


# ===================================================================
# doxygen 起動用のコマンド
# ===================================================================
