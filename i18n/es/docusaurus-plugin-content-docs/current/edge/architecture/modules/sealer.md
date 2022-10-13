---
id: sealer
title: Sealer
description: Explicación para el módulo Sealer de Polygon Edge.
keywords:
  - docs
  - polygon
  - edge
  - architecture
  - module
  - sealer
  - sealing
---

## Resumen {#overview}

El **Sealer** es una entidad que reúne las transacciones y crea un nuevo bloque.<br />
 Luego, ese bloque se envía al módulo **Consensus** para sellarlo.

La lógica de sellado final se encuentra dentro del módulo **Consensus**.

## Ejecutar Método {#run-method}

````go title="sealer/sealer.go"
func (s *Sealer) run(ctx context.Context) {
	sub := s.blockchain.SubscribeEvents()
	eventCh := sub.GetEventCh()

	for {
		if s.config.DevMode {
			// In dev-mode we wait for new transactions to seal blocks
			select {
			case <-s.wakeCh:
			case <-ctx.Done():
				return
			}
		}

		// start sealing
		subCtx, cancel := context.WithCancel(ctx)
		done := s.sealAsync(subCtx)

		// wait for the sealing to be done
		select {
		case <-done:
			// the sealing process has finished
		case <-ctx.Done():
			// the sealing routine has been canceled
		case <-eventCh:
			// there is a new head, reset sealer
		}

		// cancel the sealing process context
		cancel()

		if ctx.Err() != nil {
			return
		}
	}
}
````

:::caution Trabajo en progreso

Los módulos **Sealer** y **Consensus** se combinarán en una sola entidad en un futuro próximo.

El nuevo módulo incorporará una lógica modular para diferentes tipos de mecanismos consensus que requieren diferentes implementaciones de sellado:
* **PoS** (Prueba de Participación)
* **PoA** (Prueba de Autoridad)

Actualmente, los módulos **Sealer** y **Consensus** funcionan con PoW (Prueba de Funcionamiento).

:::