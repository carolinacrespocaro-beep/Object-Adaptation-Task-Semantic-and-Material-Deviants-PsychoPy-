# Object Adaptation Task: Semantic and Material Deviants (PsychoPy)

A PsychoPy experiment on repetition-based adaptation to everyday objects.
Participants watch rapid sequences of images of the same object (adaptation phase),
followed by a deviant object that is either semantically close or semantically
distant to the adapter, and that either shares or differs in material.
Participants press SPACE whenever they notice a different object.

## Task overview

Each trial has two phases:

1. **Adaptation**: 5 to 9 images of the same object (same material folder), shown
   one at a time (400 ms image, 100 ms blank). Consecutive images are never identical.
2. **Deviant**: 4 images of a different object (400 ms image, 100 ms blank), chosen
   according to the trial condition.

### Design

| Factor | Levels |
|---|---|
| Adapter object | 7 (bucket, bottle, spoon, fork, jug, grater, hanger) |
| Adaptation length | 5, 6, 7, 8, 9 repetitions |
| Semantic relation | SC / SD (deviant defined per adapter in `stimuli_relations`) |
| Material | Same / Different from the adapter |
| Repetitions per cell | 4 |

7 objects × 5 lengths × 4 conditions × 4 repetitions = **560 trials**, fully randomised,
with two breaks (after trials 187 and 373).

## Requirements

- Python 3.8+
- [PsychoPy](https://www.psychopy.org/)
- pandas
- openpyxl (for `.xlsx` output)

```bash
pip install psychopy pandas openpyxl
```

## Stimuli structure

Images must be organised as `<base_path>/<object>/<material>/*.png|jpg`:

```
Objetos/
├── bucket/
│   ├── metal/
│   │   ├── img1.png
│   │   └── ...
│   └── plastic/
├── bottle/
└── ...
```

Folder names must match the object names in `stimuli_relations` (case-insensitive),
including every deviant object (e.g. `nutcraker`, `door handle`).

## Usage

1. Edit `base_path` in `exp_objetos.py` to point to your stimuli folder.
2. Run the script:
   ```bash
   python exp_objetos.py
   ```
3. Enter the participant ID and session in the dialog.
4. Press **ESC** at any time to quit; partial data are saved automatically.

## Output

Results are saved in `00.Resultados/`:

- `res_<ID>_<session>.xlsx`: full data (one row per trial)
- `Parcial_<ID>.xlsx`: saved if the experiment is aborted with ESC

| Column | Description |
|---|---|
| `N_Trial` | Trial number |
| `Objeto_Adaptador` | Adapter object |
| `Objeto_Deviante` | Deviant object |
| `Relacao_Semantica` | SC or SD |
| `Condicao_Material` | Mesmo (same) or Diferente (different) |
| `Pasta_Material_Original` | Material folder used in adaptation |
| `Num_Repeticoes_Adapt` | Number of adapter images (5 to 9) |
| `Respostas_RT_String` | Key presses: `FAlarme_<t>` (false alarm during adaptation, time from trial start) and `Dev<n>_RT_<t>` (response to deviant image n, RT from deviant onset, in seconds) |

## Notes

- Instructions shown to participants are in European Portuguese.


## Citation and licence

Add your licence (e.g. MIT) and, if applicable, how to cite this task.
