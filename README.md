import com.sun.speech.freetts.Voice;
import com.sun.speech.freetts.VoiceManager;

public class VoiceChanger {

    public static void main(String[] args) {
        // Specify the text you want to convert to speech
        String text = "Hello, this is a test.";

        // Select a voice
        String voiceName = "kevin16"; // You can change this to the desired voice

        // Create a VoiceManager instance
        VoiceManager voiceManager = VoiceManager.getInstance();

        // Get the available voices
        Voice[] voices = voiceManager.getVoices();

        // Find the selected voice
        Voice selectedVoice = null;
        for (Voice voice : voices) {
            if (voice.getName().equals(voiceName)) {
                selectedVoice = voice;
                break;
            }
        }

        // If the selected voice is found, use it; otherwise, use the default voice
        if (selectedVoice != null) {
            selectedVoice.allocate();
            selectedVoice.speak(text);
            selectedVoice.deallocate();
        } else {
            System.out.println("Voice not found. Using default voice.");
            Voice defaultVoice = voiceManager.getVoice(voiceManager.getVoices()[0].getName());
            defaultVoice.allocate();
            defaultVoice.speak(text);
            defaultVoice.deallocate();
        }
    }
}

