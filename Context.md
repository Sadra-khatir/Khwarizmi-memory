# Project Context

## Project
AI football analyzer: low-cost, post-match, player-centric tactical analysis from a single fixed camera. For amateur/lower-league teams in Iran.

## Event
Khwarizmi Festival (about 10 months).

## Team
- Kooroush Muhammady: (role)
- Sadra: (role)

## Core design (from the redesign report, 7 Nov 2026)
- Offline post-match processing, NOT live streaming (live was dropped: more complex, less accurate, no proven need)
- Player-centric first; the ball is the riskiest part and sits behind a gate
- Pipeline: video -> player detector (YOLO11s, RF-DETR-S as comparison) -> ByteTrack-style tracker -> team clustering (LAB + K-means) -> manual homography (4-8 points) -> pitch coordinates -> offline smoothing + tracklet stitching -> CSV/Parquet + Persian HTML report
- Hardware: laptop with RTX 3050 (4 GB VRAM), batch processing. Phone is for recording only.
- Target: full 90-min game processed in about 2.5 hours (an estimate, not measured)

## MVP-1 (no ball, about 14 weeks)
Heatmaps, distance/speed with error bars, team shape, minimap video, Persian HTML report. Not included: ball, possession, passes, shots, live, cloud.

## Phases and gates
P0 validation (record 1 real game, measure pixel sizes, 5-10 coach interviews) -> G0
P1 prototype -> P2 baseline accuracy (G1) -> P3 MVP-1 (G2) -> P4 ball (G3) -> P5 possession/events -> P6 research.
Failing a gate means stop, simplify or redefine.

## Research question
Does confidence-triggered detection scheduling keep final coach-facing stats (distance, heatmap, team shape) accurate at lower compute than fixed stride, and when does the error exceed human labeling noise?
Honest claim: not a new method; value is local data, offline use on cheap hardware, Persian UI.

## Rules
- Label every estimate as an estimate, with uncertainty
- Never claim "first in Iran" or unmeasured FPS/accuracy
- Mark unverified items; don't guess

## Rules for working with AI
- Keep answers short and precise
- If unsure, say so, don't guess
- Answer in Persian unless asked otherwise
