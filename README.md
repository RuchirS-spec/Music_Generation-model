# AI Music Generation with PyTorch & music21 🎹

This project uses a Recurrent Neural Network (RNN), specifically an LSTM (Long Short-Term Memory) model, to generate new musical melodies. The model is built with **PyTorch** and processes MIDI files using the **`music21`** library.

It learns the patterns, melodies, and harmonic structures from a given set of MIDI files and then composes a new, original piece of music in a similar style.

---

## 🚀 How It Works

The entire process is contained within the `AI_Music_Generation_Notebook.ipynb` file and follows these key steps:

### 1. Data Preprocessing

* **Melody Extraction:** The script first parses a directory of multi-track MIDI files. It intelligently identifies the main melody from each song, which is typically the track with the highest average pitch (often the vocal or lead instrument line).
* **Vocabulary Creation:** It creates a "vocabulary" of all unique musical events (notes like `C#4`, chords like `60.64.67`, and rests).
* **Sequence Generation:** The continuous stream of musical events is then broken down into smaller, fixed-length sequences. The model is trained on these sequences to predict the next event given the preceding ones.

### 2. Model Architecture

* The core of the project is a **stacked LSTM network**.
* An **Embedding Layer** converts the numerical representation of each note/chord into a dense vector, allowing the model to learn relationships between them.
* The **LSTM Layers** process the sequences, capturing temporal dependencies and learning the "rules" of the musical style.
* A final **Linear Layer** with a Softmax function outputs a probability distribution over the entire vocabulary to predict the next musical event.

### 3. Training

* The model is trained on the prepared sequences for a specified number of epochs.
* It uses the Adam optimizer and Cross-Entropy Loss to adjust its weights, progressively getting better at predicting the next note in a sequence.
* Checkpoints are saved periodically, and the final trained model is stored for later use.

### 4. Music Generation

* To generate a new song, the model is seeded with a random sequence from the original dataset.
* It then predicts the next note, appends it to the sequence, and uses the updated sequence as the input for the next prediction.
* This process is repeated hundreds of times to create a full-length melody.
* Finally, the generated sequence of musical events is converted back into a playable **MIDI file** using `music21`.

---

## 🛠️ How to Use

This project is designed to be run as a Google Colab notebook.

1.  **Open the Notebook:** Load `AI_Music_Generation_Notebook.ipynb` in Google Colab.
2.  **Set Runtime to GPU:** For significantly faster training, navigate to `Runtime` -> `Change runtime type` and select `GPU` as the hardware accelerator.
3.  **Run Cell 1 (Setup):** This will install `music21` and import all necessary libraries.
4.  **Run Cell 2 (Configuration & Data Upload):**
    * This cell defines the model's hyperparameters.
    * It will prompt you to **upload your dataset of MIDI files**.
5.  **Run Cell 3 (Preprocessing):** This will process all your uploaded MIDI files and prepare them for the model.
6.  **Run Cell 4 (Define Model):** This defines the LSTM model class.
7.  **Run Cell 5 (Train the Model):** This is the most time-consuming step. The model will train on your data, and you will see the loss decrease with each epoch.
8.  **Run Cell 6 (Generate Music):** Once training is complete, this cell will use your trained model to generate a new song and save it as `ai_generated_song.mid` in the Colab file browser. You can then download and listen to your creation!
