# CarND-Controls-PID
Self-Driving Car Engineer Nanodegree Program

---

## Dependencies

* cmake >= 3.5
 * All OSes: [click here for installation instructions](https://cmake.org/install/)
* make >= 4.1
  * Linux: make is installed by default on most Linux distros
  * Mac: [install Xcode command line tools to get make](https://developer.apple.com/xcode/features/)
  * Windows: [Click here for installation instructions](http://gnuwin32.sourceforge.net/packages/make.htm)
* gcc/g++ >= 5.4
  * Linux: gcc / g++ is installed by default on most Linux distros
  * Mac: same deal as make - [install Xcode command line tools]((https://developer.apple.com/xcode/features/)
  * Windows: recommend using [MinGW](http://www.mingw.org/)
* [uWebSockets](https://github.com/uWebSockets/uWebSockets)
  * Run either `./install-mac.sh` or `./install-ubuntu.sh`.
  * If you install from source, checkout to commit `e94b6e1`, i.e.
    ```
    git clone https://github.com/uWebSockets/uWebSockets
    cd uWebSockets
    git checkout e94b6e1
    ```
    Some function signatures have changed in v0.14.x. See [this PR](https://github.com/udacity/CarND-MPC-Project/pull/3) for more details.
* Simulator. You can download these from the [project intro page](https://github.com/udacity/self-driving-car-sim/releases) in the classroom.

There's an experimental patch for windows in this [PR](https://github.com/udacity/CarND-PID-Control-Project/pull/3)

## Basic Build Instructions

1. Clone this repo.
2. Make a build directory: `mkdir build && cd build`
3. Compile: `cmake .. && make`
4. Run it: `./pid`.

## Reflections

### The effect each of the P, I, D components had in your implementation

#### P (Proportional)
Steer in proportion to the cross track error. If the term is too high there will be oscillations. If the value is too low there won't be enough error correction and the vehicle will fall off track.

#### I (Integral)
The sum of the cross track error over time. This is for correcting systemic biases. If this term is too low then the car will slowly drift on one side of the road. If the term is too high you will be having more oscillations.

#### D (Derivative)
Change in CTE from one value to another, thus named derivative. This term adds to counter steering to make up for overshooting caused by P. When the term is too low the vehicle will quickly stray out of bounds as a consequence of not having enough counter steering. When the term is too high, although the vehicle would stay centered on the road, it would also waste more throttle constantly steering left and right.

### How the final hyperparameters were chosen
I used used the manual tuning method, trying different values with the command line arguments and seeing how the performance in the simulator was.

i.e.
```
double init_Kp = atof(argv[1]);
double init_Ki = atof(argv[2]);
double init_Kd = atof(argv[3]);
```

Ultimately the vehicle was able to make a safe passage around the track, albeit probably causing the passengers to get sick during the drive. Certainly there could be a lot more tweaking of the parameters and perhaps getting more creative with throttle control would also help.
