# Ultracortex EEG 2024 Dataset

## Dataset Description
The Ultracortex EEG 2024 dataset was collected using the Ultracortex Mark IV EEG Headset on six subjects in two separate sessions, in collaboration with the REDRAW project and the Institute of Biostructures and Bioimaging (IBB-CNR). The main objective was to evaluate the effectiveness of Federated Learning in preserving the privacy of sensitive subject data while building a robust machine learning model for mental activity classification.

## Folder Content
- **raw_data**: Contains the raw EEG data acquired directly from the headset.
- **preprocessed_data**: Contains the preprocessed files in numpy format, divided into training and test sets.

## Data Collection
During each session, participants were instructed to imagine the movement of the left hand, the right hand, or to not imagine any movement (control class). Each session involved a variable number of runs, with each run consisting of 11 trials.

### Data Collected per Session
| Subject | Session 1 | Session 2 |
|---------|-----------|-----------|
| User 1  | 110       | 55        |
| User 2  | 99        | 55        |
| User 3  | 110       | 66        |
| User 4  | 99        | 55        |
| User 5  | 99        | 44        |
| User 6  | 88        | 44        |
| **Total** | **704** | **374**   |

## File Format
The recordings of each trial are saved as `mne` objects using the MNE library from MOABB. Each file contains a variable number of samples, depending on the sampling rate, with data from the 16 EEG channels.

### Folder Structure
The records are organized by subject, with a division into two folders corresponding to the two recording sessions. Within each session, files are grouped into three folders, one for each class:
- **Class 0**: Imagination of moving the left hand.
- **Class 1**: Imagination of moving the right hand.
- **Class 2**: No movement imagination (control class).

## Test Execution
The test was performed following a visual prompt presented to the subject, consisting of four phases: preparation, presentation of the visual cue, task execution, and pause. Each run consisted of 11 trials, with a short interval between runs.

### Test Phases
1. **Preparation**: A cross appeared on the screen with an acoustic signal.
2. **Presentation of the Visual Cue**: A left arrow, right arrow, or circle appeared for 1.25 seconds.
3. **Task Execution**: The subject imagined the movement indicated by the cue for 3 seconds.
4. **Pause**: A brief pause between trials.

## Preprocessed Dataset
The dataset was built by combining the data from the first and second sessions, with 20% of the total used as the test set. Only classes 0 and 1 were used for training and testing. The distribution of samples per subject and class was balanced.

### Preprocessing Techniques
The preprocessing techniques used to create the preprocessed dataset include:
1. **Resampling**: Reducing the number of samples to 750, equivalent to a sampling rate of 250 Hz.
2. **Bandpass Filter**: Applying a filter between 4 Hz and 100 Hz.
3. **Referencing**: Using the average of the channels as a reference.
4. **Normalization**: Normalizing separately for the training and test sets using z-score.
5. **Tangent Space**: Transforming the EEG data into tangent space.

### Sample Details
| Subject | Training | Test |
|---------|----------|------|
| User 1  | 98       | 25   |
| User 2  | 77       | 20   |
| User 3  | 96       | 25   |
| User 4  | 82       | 21   |
| User 5  | 75       | 19   |
| User 6  | 72       | 19   |
| **Total** | **500** | **129** |

### Sample Distribution by Class
| Subject | Training 0 | Training 1 | Test 0 | Test 1 |
|---------|------------|------------|--------|--------|
| User 1  | 47         | 51         | 12     | 13     |
| User 2  | 33         | 44         | 8      | 12     |
| User 3  | 46         | 50         | 12     | 13     |
| User 4  | 45         | 37         | 12     | 9      |
| User 5  | 38         | 37         | 10     | 9      |
| User 6  | 38         | 34         | 10     | 9      |
| **Total** | **247**  | **253**    | **64** | **65** |

## Data Collection Software
Data collection was carried out using software developed to connect the headset with the OpenBCI GUI interface and execute the test. [Data Collection Software](https://github.com/aski97/ultracortex_eeg_dataset_creator)

## Dataset Usage Example
Examples of using the dataset with both centralized and federated approaches are available:
- [Centralized and Federated Example](https://github.com/aski97/federated-learning-clients-server-simulation/tree/main/examples/ultracortex_eeg)

## Notes
Each subject signed a release form allowing the anonymous use of their EEG data.

## References
- [Data Collection Software](https://github.com/aski97/ultracortex_eeg_dataset_creator)
- [MNE](https://mne.tools/stable/index.html): Open-source library for neurophysiological data analysis.
- [MOABB](https://github.com/NeuroTechX/moabb): Mother of All BCI Benchmarks.
- [OpenBCI](https://openbci.com/): Platform for EEG signal acquisition and analysis.
