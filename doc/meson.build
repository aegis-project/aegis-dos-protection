doxygen = find_program('doxygen', required : false)
if doxygen.found()
  cdata = configuration_data()
  cdata.set('ALLOW_UNICODE_NAMES', true)
  cdata.set('CALL_GRAPH', true)
  cdata.set('COLLABORATION_GRAPH', true)
  cdata.set('CPP_CLI_SUPPORT', true)
  cdata.set('DOT_GRAPH_MAX_NODES', 20)
  cdata.set('DOT_TRANSPARENT', true)
  cdata.set('EXTRACT_ALL', true)
  cdata.set('EXTRACT_PACKAGE', true)
  cdata.set('EXTRACT_PRIVATE', true)
  cdata.set('FULL_PATH_NAMES', false)
  cdata.set('GENERATE_TREEVIEW', true)
  cdata.set('HAVE_DOT', true)
  cdata.set('HIDE_UNDOC_RELATIONS', false)
  cdata.set('HTML_EXTRA_STYLESHEET', join_paths(meson.current_source_dir(),'doxygen-extra.css'))
  cdata.set('HTML_TIMESTAMP', true)
  cdata.set('OUTPUT_DIRECTORY', join_paths(meson.project_build_root(), 'doc'))
  cdata.set('PLANTUML_JAR_PATH', join_paths(meson.current_source_dir(), 'plantuml.jar'))
  cdata.set('PLANTUML_CFG_FILE', join_paths(meson.current_source_dir(), 'plantuml-config.txt'))
  cdata.set('PROJECT_DOCDIR', meson.current_source_dir())
  cdata.set('PROJECT_EXAMPLESDIR', join_paths(meson.project_source_root(),'examples'))
  cdata.set('PROJECT_INCDIR', join_paths(meson.project_source_root(),'include'))
  cdata.set('PROJECT_LOGO', join_paths(meson.current_source_dir(), 'img', 'doxygen_logo.png'))
  cdata.set('PROJECT_NAME', meson.project_name())
  cdata.set('PROJECT_SRCDIR', join_paths(meson.project_source_root(),'source'))
  cdata.set('PROJECT_TESTDIR', join_paths(meson.project_source_root(),'test'))
  cdata.set('RECURSIVE', true)
  cdata.set('SOURCE_BROWSER', true)
  cdata.set('TEMPLATE_RELATIONS', true)
  cdata.set('TREEVIEW_WIDTH', 200)
  cdata.set('UML_LIMIT_NUM_FIELDS', 100)
  cdata.set('UML_LOOK', true)
  cdata.set('USE_MATHJAX', true)
  cdata.set('VERSION', meson.project_version())

  doxyfile = configure_file(input: 'Doxyfile.in',
                            output: 'Doxyfile',
                            configuration: cdata,
                            install: false)
  docdir = join_paths(get_option('datadir'),'doc', meson.project_name())
  html_target = custom_target('doc',
                            build_always_stale: true,
                            input: doxyfile,
                            output: 'html',
                            command: [doxygen, doxyfile, meson.project_source_root()],
                            install: true,
                            install_dir: docdir,
                            build_by_default: true)
else
  warning('Documentation disabled without doxygen')
endif
