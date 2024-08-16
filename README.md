# sea-dropfrom pydub import AudioSegment
from pydub.playback import play
import numpy as np

def generate_droplet_sound():
    sample_rate = 44100
    
    # Define the parameters for the droplet sound
    freq = 1000  # frequency of the tone
    duration_ms = 200  # duration of the droplet sound
    decay_factor = 0.5  # how quickly the sound fades out
    
    t = np.linspace(0, duration_ms / 1000, int(sample_rate * duration_ms / 1000), False)
    
    # Create a sine wave that fades out (decays)
    sine_wave = np.sin(2 * np.pi * freq * t) * np.exp(-decay_factor * t)
    
    # Convert to 16-bit audio format
    audio = np.int16(sine_wave * 32767)
    
    # Create an audio segment from the generated tone
    droplet_sound = AudioSegment(audio.tobytes(), frame_rate=sample_rate, sample_width=2, channels=1)
    
    return droplet_sound

# Generate the droplet sound
droplet_sound = generate_droplet_sound()

# Play the droplet sound
play(droplet_sound)
