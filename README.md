# Multi-Compartment VRPSPD Instances

Instances for the multi-compartment Vehicle Routing Problem with Simultaneous Pickup and Delivery (VRPSPD), in which each vehicle has one dedicated compartment per product. They were created for the study in [paper reference, to be added upon publication], but can be used for any multi-compartment VRPSPD variant.

## Instance sets

- **nkXX** (`nk01`–`nk05`): small, randomly generated instances.
- **CMT instances** (e.g., `CMT1X(55)`): adapted from the VRPSPD benchmark instances of Salhi and Nagy [1]. Each customer's delivery and pickup quantities, and the vehicle capacity, are split over the products using the same ratio vector. The digits in parentheses give this ratio in tenths, e.g., `CMT1X(55)` uses a 50/50 split over two products, and `CMT3X(433)` a 40/30/30 split over three products, and so on.
- **Heterogeneous product-mix instances** (`mix/`, e.g., `CMT2X(37)-H50`): derived from eight of the CMT instances. They keep the coordinates, fleet, compartment capacities, and each customer's total delivery and pickup quantities of the base instance, and only change how these totals are split over the products. The suffix `-H<100h>` gives the heterogeneity level h, i.e., how far the customers' product mixes deviate from the compartment proportions (h = 0 is the base instance). The construction is described in the comment line of each file and in the accompanying paper.

## File format

The files follow a TSPLIB-style text format. Lines starting with `#` are comments.

**Header**
- `NAME`: instance name.
- `TYPE`: `VRPSPD_MC`.
- `DIMENSION`: number of nodes, including the depot.
- `VEHICLES`: number of available (identical) vehicles.
- `PRODUCTS`: number of products, which equals the number of compartments of each vehicle.
- `CAPACITY`: capacity of each compartment of a vehicle, one value per product.
- `EDGE_WEIGHT_TYPE`: `EXACT_2D`, i.e., the travel cost between two nodes is their Euclidean distance, without rounding.

**NODE_COORD_SECTION**: one line per node, `i x y`.

**PICKUP_AND_DELIVERY_SECTION**: one line per node, `i e l H s d1 p1 d2 p2 … dP pP`, where `dk` and `pk` are the delivery and pickup quantities of product k at node i. The fields `e`, `l`, `H`, and `s` (time window, horizon, and service time) are placeholders and are not used as our version of the problem has no time windows. The depot row has all quantities equal to 0.

**DEPOT_SECTION**: node 1 is the unique depot, followed by `-1`. The file ends with `EOF`.

## Interpretation

- Compartments are dedicated: the capacity of a compartment can only be used by its product, and unused space cannot be shared between products.
- All vehicles are identical, and the fleet size is given by `VEHICLES`.

In the accompanying paper, deliveries are mandatory, pickups are optional (each product's pickup at a customer is collected in full or not at all), and the two objectives are to minimize the routing cost and to maximize the collected pickup volume.

## Reference

[1] Salhi, S., Nagy, G.: A cluster insertion heuristic for single and multiple depot vehicle routing problems with backhauling. Journal of the Operational Research Society 50(10), 1034–1042 (1999).

If you use these instances, please cite: [paper reference, to be added upon publication].
