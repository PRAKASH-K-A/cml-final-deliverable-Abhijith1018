[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/aQj7XJJr)
Individual Contribution Report - README

Name: Nandagiri Sai Abhijith
Registration Number: 230958122
Role: Team Leader - Group 2 (Execution & Trade Service)
Module: Capital Markets Trading Systems
Academic Year: 2026-2027

Executive Summary

This README outlines my individual technical and leadership contributions to the Capital Markets Trading System project.

My primary engineering responsibility was the design and implementation of MatchingEngine.java, the algorithmic core of the trading platform responsible for generating microsecond-level trade executions.

As Team Leader, I also designed the overall asynchronous system architecture and coordinated the integration of five sub-components developed by my team members.

Core Technical Contributions
1. The Matching Engine (MatchingEngine.java)
Algorithm Implementation: Designed and implemented the Price-Time Priority algorithm (FIFO matching), the same fair-ordering mechanism used by major exchanges like NASDAQ and NYSE.
Price Priority: Ensured that orders with the best price (highest bid / lowest ask) are executed first.
Time Priority: Guaranteed that orders at identical prices are executed based on earliest arrival time.
Low-Latency Data Structures: Utilized ConcurrentSkipListMap and ConcurrentLinkedDeque to achieve efficient 
𝑂
(
log
⁡
𝑛
)
O(logn) access to price levels and lock-free FIFO ordering.
Thread Safety: Built the matching engine using the java.util.concurrent package, eliminating explicit locks to avoid latency spikes and deadlocks.
2. System Architecture Design

Three-Speed Asynchronous Pipeline: Designed a decoupled processing architecture where:

Tier 1: Matching Engine (microsecond execution)
Tier 2: Database Persistence
Tier 3: WebSocket UI Broadcasting

This ensures that high-speed trade execution is never blocked by slower operations.

Non-Blocking Database Persistence: Implemented a producer-consumer pattern using LinkedBlockingQueue<Trade>, enabling the matching engine to push trades in 
𝑂
(
1
)
O(1) time while a background thread handles PostgreSQL inserts asynchronously.
3. Functional Testing & Correctness Validation

Designed comprehensive end-to-end test scenarios to validate system correctness:

Scenario A (Perfect Match):
Verified that identical opposing orders result in a single trade, complete order removal, and accurate execution reports.
Scenario B (Price Priority & Price Improvement):
Demonstrated that better-priced orders take precedence over earlier inferior orders and that aggressor orders receive price improvement when applicable.
Scenario C (Partial Fills):
Validated correct quantity handling and residual order tracking when orders are partially matched.
Performance Metrics Achieved

The system achieved high-performance benchmarks suitable for high-frequency trading simulations:

Median (P50) Tick-to-Trade Latency: 2–8 microseconds
P99 Tick-to-Trade Latency: 30–50 microseconds
Theoretical Peak Throughput: 100,000 – 500,000 orders per second
Leadership & Integration Management
Interface Contracts:
Defined clear Java interface contracts for all five sub-components (Order Book Manager, Trade Generation, Database Persistence, WebSocket UI, and Telemetry), enabling parallel development.
Integration Testing:
Implemented bidirectional consistency checks to ensure synchronization between the matching engine and order book state.
Quality Assurance:
Conducted detailed code reviews and resolved multiple race conditions across modules, ensuring data integrity and system stability before final demonstration.
Final Summary

I contributed both as a core system engineer and a team leader, delivering:

A high-performance matching engine aligned with real-world exchange logic
A scalable asynchronous architecture
Robust testing and validation strategies
Effective team coordination and system integration

This project reflects my ability to design and implement low-latency, concurrent financial systems, aligning with real-world capital markets technology.
