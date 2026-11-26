# ha-controller-architecture
A reusable capability-based controller architecture for Home Assistant, separating control intent, execution permission, and device operation. Includes reference blueprints and configuration examples accompanying the Home Assistant Community article.

*This repository was prepared with the assistance of ChatGPT in organizing, writing, and translating my ideas. There might be some mistakes.*

# A Reusable Capability-Based Controller Architecture for Home Assistant

Separating control intent, execution permission, and device operation.

## Overview

This repository accompanies my article on a capability-based controller architecture for Home Assistant. It contains reference blueprints and configuration examples adapted from my personal Home Assistant system.

The architecture separates what a device should do from whether automatic execution is permitted and how the device is operated. A capability may have a baseline **Target**, an optional **Override**, and an **Execution Gate**. The effective target is resolved from the applicable decision inputs. Controllers evaluate execution conditions and act on relevant events rather than continuously enforcing the desired state.

The examples illustrate how these design principles can be reused across lighting, circulation fans, and curtains without requiring identical controller implementations.

## Related article

*A Reusable Capability-Based Controller Architecture for Home Assistant* — Home Assistant Community. The article link will be added upon publication.

## Reference files

### Core controllers

| File | Purpose |
| --- | --- |
| [Power Controller](blueprints/controllers/power_controller_bp.yaml) | Resolves power intent and supports simple and profile-aware activation. |
| [Profile Controller](blueprints/controllers/profile_controller_bp.yaml) | Applies lighting profiles when execution is permitted and applicable. |
| [Fan Power Controller](blueprints/controllers/fan_power_controller_bp.yaml) | Handles fan power intent and profile-aware activation. |
| [Fan Profile Controller](blueprints/controllers/fan_profile_controller_bp.yaml) | Handles fan profile updates. |
| [Curtain Controller](blueprints/controllers/curtain_controller_bp.yaml) | Executes position targets using a positive auto gate, movement-state checks, and position tolerance. |

### Supporting mechanisms

| File | Purpose |
| --- | --- |
| [Minimum Guard](blueprints/supporting/power_min_guard_bp.yaml) | Uses actual power transitions to manage a minimum-on timer. |
| [Automatic Pause Clear](blueprints/supporting/auto_pause_clear_bp.yaml) | Illustrates context-based release of manual control restrictions. |
| [Curtain Manual Detection](blueprints/supporting/curtain_manual_bp.yaml) | Infers manual movement using running-state transitions and an automatic movement attribution token. |

### Implementation examples

| File | Purpose |
| --- | --- |
| [Balcony Lighting](examples/lighting/balcony_light_pack.yaml) | Single-capability power control, illuminance guard, and minimum-on behavior. |
| [Living Room Main Lighting](examples/lighting/living_main_pack.yaml) | Separate power and profile decisions for a virtual light. |
| [Living Room Shared Configuration](examples/lighting/living_common_pack.yaml) | Reference excerpt showing shared execution restrictions, illuminance guards, and composition interfaces. |
| [Kitchen Circulation Fan](examples/ventilation/fan_kitchen_controller_pack.yaml) | Power and profile targets derived from airflow demand and environmental conditions. |
| [Guest Curtain](examples/curtain/curtain_pack.yaml) | Reference excerpt showing position targets, a positive execution gate, and manual movement detection. |

## Notes on the reference configurations

These files are intended for reading alongside the article. They are **not standalone, ready-to-install packages** or a complete Home Assistant configuration.

- Original entity IDs, blueprint references, and device-specific parameters are generally retained. Repository paths are organized for reading and do not necessarily match the original deployment paths.
- Display names, descriptions, comments, and diagnostic messages have been translated into English where applicable. Selected configurations have been excerpted and minor corrections made for publication.
- External dependencies are intentionally retained where they illustrate architectural boundaries. Presence processing, composition decisions, virtual device definitions, actuator execution scripts, and parts of the curtain position assignment and reset logic are outside the scope of this repository.
- The curtain controller and manual detection blueprints illustrate a short-lived attribution token, not a guaranteed identification of command origin.
- The published excerpts have not been tested as a standalone Home Assistant configuration. Review and adapt them before using them in another system.

## License

See [LICENSE](LICENSE) for the license applicable to the files in this repository.
