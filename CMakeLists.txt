cmake_minimum_required(VERSION 3.22)
project(AQWAX VERSION 1.0.0)

# Point JUCE_DIR to your JUCE installation, e.g.
# cmake -S . -B build -DJUCE_DIR="C:/JUCE"
if(NOT DEFINED JUCE_DIR)
    message(FATAL_ERROR "Please set JUCE_DIR to your JUCE folder.")
endif()

add_subdirectory("${JUCE_DIR}" JUCE)

juce_add_plugin(AQWAX
    COMPANY_NAME "AQWAX"
    BUNDLE_ID "com.aqwax.plugin"
    PLUGIN_MANUFACTURER_CODE AqWx
    PLUGIN_CODE Aqw1
    FORMATS VST3
    PRODUCT_NAME "AQWAX"
    IS_SYNTH FALSE
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MIDI_EFFECT FALSE
    COPY_PLUGIN_AFTER_BUILD TRUE
)

target_sources(AQWAX PRIVATE
    Source/PluginProcessor.cpp
    Source/PluginProcessor.h
    Source/PluginEditor.cpp
    Source/PluginEditor.h
)

target_compile_features(AQWAX PRIVATE cxx_std_17)

target_link_libraries(AQWAX PRIVATE
    juce::juce_audio_utils
    juce::juce_dsp
    juce::juce_recommended_config_flags
    juce::juce_recommended_lto_flags
    juce::juce_recommended_warning_flags
)

juce_generate_juce_header(AQWAX)
