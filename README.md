# PhaseLands

Прототип экшен-RPG от третьего лица на **Unreal Engine 5.8** (чистый Blueprint-проект, без C++).

Внутренние рабочие названия: `Rogue Character` / `Rogue_51`.

## Об игре

Third-person action RPG с открытым миром: ближний бой (катана, двуручный меч), стрельба из лука с прицеливанием, магия (книга заклинаний, Chain Lightning), блок/парирование/уклонения, способности с кулдаунами (Rain of Arrows и др.), крафт, лут с редкостью, торговцы, диалоги, боссы и живой мир (волки, олени, враждебные фракции).

## Игровые системы

| Система | Описание |
|---|---|
| **Комбат** | Ближний/дальний/магический бой, блок, парирование, уклонение, hit-react по направлениям, стан, состояния неуязвимости |
| **Способности** | `BPC_Abilities` + `BPC_CooldownAbility`, данные в `DT_Abilities` (Chain Lightning, Rain of Arrows, ...) |
| **ИИ врагов** | `BP_EnemyBase` → Melee / Range / Mage / Boss (`BP_Gromgard`), волки, пассивные животные, менеджер спавна (`BP_EnemyManager`), состояния ИИ, сенсоры восприятия, фракции |
| **RPG-предметы** | Редкость, таблицы лута, случайные статы, крафт (`E_Recipes`, `S_Craft`), ключевые предметы, быстрые слоты |
| **NPC и экономика** | Торговец (`BP_Trader`), диалоги, продажи (`S_ItemsToSell`) |
| **UI/UX** | HUD игрока, инвентарь, статы, апгрейды, босс-бары, тултипы, плавающий урон, NotifyBox |
| **Прогресс** | Атрибуты, условия/эффекты (`DT_Conditions`, `DT_Effects`), Save-система (`BP_Save` + `BP_GameInstanceCore`) |
| **Мир** | Крупные ландшафты с World Partition и HLOD (`L_Waldingbury`, `L_Hub`), вода (Water plugin + Landmass), PCG-насаждение, кастомный ландшафтный автоматериал, погодные/атмосферные эффекты |

## Карты

- `L_Waldingbury` — основная большая локация (ландшафт, HLOD)
- `L_Hub` — хаб-локация
- `L_Dev` — девелоперская карта (стартовая при открытии проекта)
- `L_Main`, `L_Water`, `RoguePreviewMap` — вспомогательные

## Структура проекта

```
PhaseLands/
├── Config/               # Настройки проекта (Engine, Game, Input, GameplayTags)
├── Content/
│   ├── Game/             # ★ Основная логика проекта
│   │   ├── Components/   # Компоненты: способности, атрибуты, лут, камера, ИИ...
│   │   ├── Core/         # GameInstance, Save
│   │   ├── Enemies/      # Классы врагов и боссов
│   │   ├── Enums/        # 27 энумов (E_Stats, E_Rarity, E_AiState...)
│   │   ├── Interfaces/   # Интерфейсы
│   │   ├── Levels/       # Карты
│   │   ├── NPC/          # Торговцы, базовый NPC
│   │   ├── Player/       # Меши, анимации, блюпринты игрока
│   │   ├── Structures/   # Дата-таблицы (DT_) и структуры (S_)
│   │   ├── Weapons/      # Луки, катана, двуручник, магия, щиты
│   │   └── Widgets/      # UI-виджеты
│   ├── ParagonRampage/   # Ассеты персонажа (Paragon)
│   ├── WhiteCastle/, Chaotic_Skies/, MWLandscapeAutoMaterial/  # Окружение, скайбокс, ландшафт
│   ├── AnimalVarietyPack/, Magic/, MixedVFX/, SwordTrailVFX/ ... # Место Flood/контент-паки
└── PhaseLands.uproject
```

## Требования

- **Unreal Engine 5.8** (через Epic Games Launcher)
- Git с [Git LFS](https://git-lfs.com/)
- ~35+ ГБ свободного места (LFS-объекты ~27 ГБ)

## Запуск

```bash
git lfs install
git clone https://github.com/Bullettran/PhaseLands.git
```

Открыть `PhaseLands.uproject` в UE 5.8. При первом открытии движок сгенерирует Intermediate/Binaries (для Blueprint-проекта компиляция C++ не требуется).

## Рендер

Lumen (SW ray tracing), Virtual Shadow Maps, Nanite, TSR/MSAA, DX12 (SM6). Таргет — Desktop, Scalable.

## Git и LFS

Бинарные ассеты хранятся в Git LFS (`*.uasset`, `*.umap`, `*.fbx`, `*.png`, `*.jpg`, `*.wav`, `*.raw` — см. `.gitattributes`).
Служебные папки движка (`Binaries/`, `Saved/`, `Intermediate/`, `DerivedDataCache/`) игнорируются (`.gitignore`).

> Объём LFS-хранилища ~27 ГБ — клонирование может занять длительное время и расходовать квоту GitHub LFS.

## Статус

Проект в активной разработке (прототип). Контент частично основан на платных/бесплатных маркетплейс-ассетах (Fab/Epic) — проверьте лицензии перед коммерческим использованием.
