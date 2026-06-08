cmake_minimum_required(VERSION 3.22)

project(VST Hornero VERSION 1.0.0)

set(CMAKE_CXX_STANDARD 20)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_subdirectory(libs/JUCE)

juce_add_plugin(VST Hornero
    COMPANY_NAME "Hornero"
    PLUGIN_NAME "Hornero Reverb"
    IS_SYNTH FALSE                # Es FALSE porque es un efecto (ganancia/reverb), no un instrumento
    NEEDS_MIDI_INPUT FALSE
    NEEDS_MIDI_OUTPUT FALSE
    IS_MidiEffect FALSE
    FORMATS VST3 AU               # Formatos que va a generar (VST3 para Windows/Mac, AU para Mac)
    PRODUCT_NAME "Hornero Reverb"
    
)

target_sources(VST Hornero PRIVATE
    Source/PluginProcessor.cpp
    Source/PluginProcessor.h
    Source/PluginEditor.cpp
    Source/PluginEditor.h
)

target_link_libraries(VST Hornero PRIVATE
    juce::juce_audio_utils
    juce::juce_audio_processors
    juce::juce_gui_extra
    juce::juce_recommended_config_flags
    juce::juce_recommended_lto_flags
    juce::juce_recommended_warning_flags
    juce::juce_dsp
)