cmake_minimum_required(VERSION 3.22)

project(VST_Hornero VERSION 1.0.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)


set(JUCE_VST3_CAN_REPLACE_VST2 FALSE CACHE BOOL "Disable VST2 compatibility chech" FORCE)

add_subdirectory(libs/JUCE)

juce_add_plugin(${PROJECT_NAME}
    COMPANY_NAME "Hornero"
    PLUGIN_NAME "Hornero Reverb"
    IS_SYNTH FALSE                # Es FALSE porque es un efecto (ganancia/reverb), no un instrumento
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MidiEffect FALSE
    FORMATS VST3 Standalone             # Formatos que va a generar (VST3 para Windows/Mac, AU para Mac, Standalone .exe)
    PRODUCT_NAME "Hornero Reverb"
   
    
   
)
target_sources(${PROJECT_NAME} PRIVATE
    Source/PluginProcessor.cpp
    Source/PluginProcessor.h
    Source/PluginEditor.cpp
    Source/PluginEditor.h

)


juce_generate_juce_header(${PROJECT_NAME})
target_link_libraries(${PROJECT_NAME} PRIVATE
   PRIVATE
        juce::juce_dsp
        juce::juce_core
        juce::juce_graphics
        juce::juce_gui_basics
        juce::juce_audio_utils
        juce::juce_audio_processors
        juce::juce_gui_extra
    PUBLIC
        juce::juce_recommended_config_flags
        juce::juce_recommended_lto_flags
        juce::juce_recommended_warning_flags
)