function(sherpa_add_py_test source)
  get_filename_component(name ${source} NAME_WE)
  set(name "${name}_py")

  add_test(NAME ${name}
    COMMAND
      "${PYTHON_EXECUTABLE}"
      "${CMAKE_CURRENT_SOURCE_DIR}/${source}"
  )

  get_filename_component(sherpa_path ${CMAKE_CURRENT_LIST_DIR} DIRECTORY)

  set_property(TEST ${name}
    PROPERTY ENVIRONMENT "PYTHONPATH=${sherpa_path}:$<TARGET_FILE_DIR:_sherpa>:$ENV{PYTHONPATH}"
  )
endfunction()

# please sort the files in alphabetic order
set(py_test_files
  test_hypothesis.py
  test_online_endpoint.py
  test_timestamp.py
  test_utils.py
  #
  test_endpoint_config.py
  test_endpoint_rule.py
  test_fast_beam_search_config.py
  test_feature_config.py
  test_offline_ctc_decoder_config.py
  test_offline_recognizer_config.py
  test_online_recognizer_config.py
  test_online_recognizer.py
)

foreach(source IN LISTS py_test_files)
  sherpa_add_py_test(${source})
endforeach()
