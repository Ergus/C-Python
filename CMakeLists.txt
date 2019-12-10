# Copyright (C) 2019  Jimmy Aguilar Mena

# This program is free software: you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation, either version 3 of the License, or
# (at your option) any later version.

# This program is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.

# You should have received a copy of the GNU General Public License
# along with this program.  If not, see <http://www.gnu.org/licenses/>.

cmake_minimum_required(VERSION 3.0)

project(CPython)

find_package(PythonInterp)
find_package(PythonLibs)

include_directories(${PYTHON_INCLUDE_DIRS})

configure_file(mylib.py mylib.py COPYONLY)

add_executable (main main.c)
target_link_libraries (main ${PYTHON_LIBRARIES} )

enable_testing()

add_test(test_5_4_C ./main mylib multiply 4 5)
set_tests_properties(test_5_4_C PROPERTIES
  PASS_REGULAR_EXPRESSION "Result of call: 20"
)

add_test(test_5_4_Python ./mylib.py 4 5)
set_tests_properties(test_5_4_Python PROPERTIES
  PASS_REGULAR_EXPRESSION "Result of call: 20"
)
