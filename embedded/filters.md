# Virtual filters

## Schmitt trigger
Virtual hysteresis function.

The followin example refers to hysteresis applied to upper and lower bound of control's input position.
```c
bool inDeadZone;

const float lowerBoundDistancePos = abs(self->smoothedPos - 0.0f);
const float upperBoundDistancePos = abs(self->smoothedPos - 1.0f);

const float lowerBoundDistanceTarget = abs(self->targetPos - 0.0f);
const float upperBoundDistanceTarget = abs(self->targetPos - 1.0f);

const bool isAroundLowerBoundPos = lowerBoundDistancePos < targetEps;
const bool isAroundUpperBoundPos = upperBoundDistancePos < targetEps;

const bool isAroundLowerBoundTarget = lowerBoundDistanceTarget < targetEps || self->targetPos < 0.0f;
const bool isAroundUpperBoundTarget = upperBoundDistanceTarget < targetEps || self->targetPos > 1.0f;

const bool isInLowerHysteresisBandPos = lowerBoundDistancePos < self->deadzoneMargin;
const bool isInUpperHysteresisBandPos = upperBoundDistancePos < self->deadzoneMargin;

if (
  (isAroundLowerBoundTarget && isAroundLowerBoundPos) ||
  (isAroundUpperBoundTarget && isAroundUpperBoundPos)
) {
  inDeadZone = true;
}
else if (
  (!isInLowerHysteresisBandPos && !isInUpperHysteresisBandPos) ||
  !isAroundLowerBoundTarget || !isAroundUpperBoundTarget
) {
  inDeadZone = false;
}

if (self->inDeadZone) {
	return 0.0f;
}

return controlOutput
```

## Lowpass filter
### Simple Moving Average
```c
SMA SMA_INIT(RingBuffer *ring) {
  return (SMA) {
    .ring = ring,
    .sma = 0,
    .firstRunSamples = 0,
  };
}

float SMA_SimpleMovingAverage(SMA *self, float incomingSample) {
  RING_Insert(self->ring, (uint8_t*) &incomingSample);

  if (self->firstRunSamples < self->ring->elementsNum) {
    self->sma = incomingSample;
    self->firstRunSamples++;
    return self->sma;
  }

  self->sma += (incomingSample - *((float*) RING_Get(self->ring, 0)));
  return self->sma;
}
```

### Exponential Moving Average
```c
EMA EMA_INIT(float alpha) {
  return (EMA) {
    .lastSmoothed = 0,
    .alpha = alpha,
  };
}

float EMA_ExpMovingAverage(EMA *self, float incomingSample) {
  self->lastSmoothed = self->lastSmoothed + self->alpha * (incomingSample - self->lastSmoothed);
  return self->lastSmoothed;
}
```
