# voice-into-graph-python
# imports
import matplotlib.pyplot as plt
import numpy as np
import wave, sys


# shows the sound waves
def visualize(path: str):
    # reading the audio file
    raw = wave.open(path)

    # reads all the frames
    # -1 indicates all or max frames
    signal = raw.readframes(-1)
    signal = np.frombuffer(signal, dtype="int16")

    # gets the frame rate
    f_rate = raw.getframerate()

    # to Plot the x-axis in seconds
    # you need get the frame rate
    # and divide by size of your signal
    # to create a Time Vector
    # spaced linearly with the size
    # of the audio file
    time = np.linspace(
        0,  # start
        len(signal) / f_rate,
        num=len(signal)
    )
    return time, signal;


A = visualize('Teacher.wav')
B = visualize('Student.wav')
time1 = A[0]
time2 = B[0]
signal1 = A[1]
signal2 = B[1]
print(np.size(signal1))
print(np.size(signal2))
len1 = min(np.size(signal1), np.size(signal2))
len2 = max(np.size(signal1), np.size(signal2))
if np.size(signal1) < np.size(signal2):
    index = range(len1, len2)
    print(index)
    signal2 = np.delete(signal2, index)
    time = time1
else:
    index = range(len1, len2)
    print(index)
    signal1 = np.delete(signal1, index)
    time = time2
print(type(signal1))
print(np.size(signal1))
print(np.size(signal2))
signal = abs(signal2 - signal1)
# signal = signal1
# using matplotlib to plot
# creates a new figure
plt.figure(1)

# title of the plot
plt.title("Sound Wave")

# label of x-axis
plt.xlabel("Time")

# actual plotting
plt.plot(time, signal)

# shows the plot
# in new window
plt.show()
