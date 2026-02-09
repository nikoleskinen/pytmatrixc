project('pytmatrix', 'c',
  meson_version: '>=1.10.0',
  default_options : ['warning_level=2'],
)

add_languages('fortran')

py_mod = import('python')
py = py_mod.find_installation(pure: false)
py_dep = py.dependency()

incdir_numpy = run_command(py,
  ['-c', 'import os; os.chdir(".."); import numpy; print(numpy.get_include())'],
  check : true
).stdout().strip()

incdir_f2py = run_command(py,
    ['-c', 'import os; os.chdir(".."); import numpy.f2py; print(numpy.f2py.get_include())'],
    check : true
).stdout().strip()

f2py_inputs = [
  'pytmatrix/fortran_tm/pytmatrix.pyf', 
  'pytmatrix/fortran_tm/ampld.lp.f',    
  'pytmatrix/fortran_tm/lpd.f',     
]

pytmatrix_source = custom_target('pytmatrixmodule.c',
  input: f2py_inputs,
  output : ['pytmatrixmodule.c', 'pytmatrix-f2pywrappers.f'],
  command : [py, '-m', 'numpy.f2py', '@INPUT@' ,'-m', 'pytmatrix', '--lower','--build-dir', '@OUTDIR@']
)
pytmatrix_dir = 'pytmatrix/fortran_tm'

inc_np = include_directories(incdir_numpy, incdir_f2py, pytmatrix_dir)

py.extension_module('pytmatrix',
  [
    'pytmatrix/fortran_tm/ampld.lp.f',
    'pytmatrix/fortran_tm/lpd.f',
    pytmatrix_source,
    incdir_f2py / 'fortranobject.c',
  ],
  include_directories: inc_np,
  dependencies : py_dep,
  subdir : 'pytmatrix/fortran_tm', 
  install : true
)

install_subdir('pytmatrix', 
  install_dir: py.get_install_dir(pure: false),
  exclude_files: [
    'fortran_tm/ampld.lp.f', 
    'fortran_tm/lpd.f', 
    'fortran_tm/ampld.par.f',
    'fortran_tm/pytmatrix.pyf'
  ]
)
