project('mandelbrot', 'rust',
  version : '0.1.0',
  meson_version : '>= 1.0.0',
  default_options : ['buildtype=debugoptimized',
                     'rust_std=2018',
                    ]
)

add_global_arguments(
  '-C', 'embed-bitcode=no',
  language: 'rust'
)

# trigger dependency resolution and apply dependency features in Cargo.toml.
cargo = import('rust').workspace()
pkg = cargo.package()
# cargo.package().executable('mandelbrot', install: true)

# executable() does not exist yet... for now, retrieve direct
# dependencies by hand *shrug*
num_complex_dep = cargo.subproject('num-complex').dependency()
rayon_dep = cargo.subproject('rayon').dependency()
once_cell_dep = cargo.subproject('once_cell').dependency()
async_channel_dep = cargo.subproject('async-channel').dependency()
gtk_dep = cargo.subproject('gtk4').dependency()
zerocopy_dep = cargo.subproject('zerocopy').dependency()

executable('mandelbrot', 'src/main.rs',
  rust_dependency_map : pkg.rust_dependency_map(),
  rust_args: pkg.rust_args(),
  dependencies : [gtk_dep, num_complex_dep, rayon_dep, once_cell_dep, async_channel_dep, zerocopy_dep],
  install : true,
)
