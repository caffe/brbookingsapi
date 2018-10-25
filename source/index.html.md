---
title: API Brasil Bookings

language_tabs:
  - shell

toc_footers:
  - <a href='http://www.brasilbookings.com.br'>Solicite uma API Key de desenvolvedor</a>

includes:
  - errors

search: true
---

# Introdução

Bem-vindo(a) a API do Brasil Bookings!


# Autenticação

> Para autenticação utilize o seguinte código:

```shell
curl -X GET \
  'http://app.brbookings.com/api/CAMINHODOOBJETO' \
  -H 'x-api-key:MINHAAPIKEY'
```

> Você deve substituir `MINHAAPIKEY` por sua API Key, e deve substituir `CAMINHODOOBJETO` pelo objeto que você deseja acessar.

```shell

```

A API do Brasil Bookings utiliza API Keys para autorizar o acesso à API.
A API Key deve ser informada em todos os requests ao servidor, no header da requisição, conforme o exemplo a seguir:

`X-API-KEY: MINHAAPIKEY`

<aside class="notice">
Você deve substituir <code>MINHAAPIKEY</code> com a sua API key exclusiva.
</aside>

# Tipos de Quarto

Através da rota `/rooms_api/rooms` e suas derivadas, você pode retornar os dados básicos dos tipos de quartos existentes.

## Objeto `rooms_api/rooms`

> GET https://app.brbookings.com/api/rooms_api/rooms

```json

```

> RESPOSTA (exemplo)

```json
{
  "RoomsRS": {
    "0": "Rooms",
    "Rooms": {
      "Success": "",
      "HotelCode": "1",
      "0": {
        "ID": "1",
        "Title": "Quarto 1",
        "Adults": "3",
        "Children": "2"
      },
      "1": {
        "ID": "2",
        "Title": "Quarto 2",
        "Adults": "2",
        "Children": "0"
      },
      "2": {
        "ID": "3",
        "Title": "Quarto 3",
        "Adults": "4",
        "Children": "0"
      },
      "3": {
        "ID": "4",
        "Title": "Quarto 4",
        "Adults": "5",
        "Children": "0"
      }
    }
  }
}
```

Ao consultar este método, este será o objeto que você irá receber como resposta.

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**ID** <br>integer | ID do Quarto no Brasil Bookings
**Title** <br>string | Título do quarto
**Adults** <br>integer | Quantidade máxima de ocupantes do quarto podendo ser adultos e/ou crianças
**Children** <br>integer | Quantidade máxima de ocupantes crianças do quarto

# Tipos de Tarifa

Através da rota `/rate_plans_api/rate_plans` e suas derivadas, você pode retornar os dados básicos dos tipos de tarifas existentes.

## Objeto `rate_plans_api/rate_plans`

> GET https://app.brbookings.com/api/rate_plans_api/rate_plans (exemplo)

```json

```

> RESPOSTA (exemplo)

```json
{
  "RatePlansRS": {
    "0": "Rates",
    "Rates": {
      "Success": "",
      "HotelCode": "1",
      "0": {
        "ID": "150",
        "Name": "Tarifa Padrão"
      },
      "1": {
        "ID": "151",
        "Name": "Tarifa Corporativa"
      }
    }
  }
}
```

Ao consultar este método, este será o objeto que você irá receber como resposta.

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**ID** <br>integer | ID do Tipo de Tarifa no Brasil Bookings
**Name** <br>string | Nome do tipo de tarifa

# Atualizar Disponibilidade

Através da rota `/availability_api/update_availability`, você pode atualizar a disponibilidade dos quartos por período.

## Atualizando disponibilidades

> POST https://app.brbookings.com/api/availability_api/update_availability (exemplo)

```json
{
  "AvailabilityRQ": {
    "AvailStatusMessages": {
      "HotelCode": "1",
      "AvailStatusMessage": [
        {
          "BookingLimit": "14",
          "StatusApplicationControl": {
            "Start": "2016-11-20",
            "End": "2016-11-21",
            "InvCode": "1"
          }
        },
        {
          "BookingLimit": "14",
          "StatusApplicationControl": {
            "Start": "2016-11-21",
            "End": "2016-11-22",
            "InvCode": "1"
          }
        },
        {
          "BookingLimit": "14",
          "StatusApplicationControl": {
            "Start": "2016-11-22",
            "End": "2016-11-23",
            "InvCode": "2"
          }
        }
      ]
    }
  }
}
```

> RESPOSTA (exemplo)

```json
{
  "AvailabilityRS": {
    "Success": ""
  }
}
```

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**BookingLimit** <br>integer | Quantidade de unidades disponíveis para o quarto
**Start** <br>string | Data de início da disponibilidade
**End** <br>string | Data final da disponibilidade
**InvCode** <br>string | ID do tipo de quarto no Brasil Bookings

# Atualizar Tarifas

Através da rota `/rates_api/update_rates`, você pode atualizar as tarifas dos quartos por período e número de ocupantes.

## Atualizando tarifas

> POST https://app.brbookings.com/api/rates_api/update_rates (exemplo)

```json
{
  "RatesRQ": {
    "RatePlans": {
      "HotelCode": "1",
      "RatePlan": {
        "RatePlanCode": "1",
        "Rates": {
          "Rate": [
            {
              "Start": "2016-11-28",
              "End": "2016-11-29",
              "InvCode": "1",
              "BaseByGuestAmts": {
                "BaseByGuestAmt": [
                  {
                    "Amount": "150.00",
                    "NumberOfGuests": "1"
                  },
                  {
                    "Amount": "20.00",
                    "NumberOfGuests": "2"
                  },
                  {
                    "Amount": "30.00",
                    "NumberOfGuests": "3"
                  }
                ]
              }
            }
          ]
        }
      }
    }
  }
}
```

> RESPOSTA (exemplo)

```json
{
  "RatesRS": {
    "Success": ""
  }
}
```

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**RatePlanCode** <br>integer | ID do tipo de tarifa
**Start** <br>string | Data de início da disponibilidade
**End** <br>string | Data final da disponibilidade
**InvCode** <br>string | ID do tipo de quarto no Brasil Bookings
**Amount** <br>float | Valor da tarifa
**NumberOfGuests** <br>integer | Número de ocupantes da tarifa

# Atualizar Restrições e Estadia Mínima

Através da rota `/restrictions_api/update_restrictions`, você pode atualizar as restrições e estadias mínimas dos quartos por período e tipo de tarifa.

## Atualizando restrições e estadias mínimas

> POST https://app.brbookings.com/api/restrictions_api/update_restrictions (exemplo)

```json
{
  "RestrictionsRQ": {
    "AvailStatusMessages": {
      "HotelCode": "1",
      "AvailStatusMessage": [
        {
          "StatusApplicationControl": {
            "Start": "2016-11-02",
            "End": "2016-11-03",
            "RatePlanCode": "1",
            "InvCode": "1"
          },
          "LengthsOfStay": {
            "LengthOfStay": {
              "Time": "3",
              "TimeUnit": "Day",
              "MinMaxMessageType": "MinLOS"
            }
          }
        },
        {
          "StatusApplicationControl": {
            "Start": "2016-11-02",
            "End": "2016-11-03",
            "RatePlanCode": "1",
            "InvCode": "1"
          },
          "RestrictionStatus": [{
              "Restriction": "Arrival",
              "Status": "Open"
            },
            {
              "Restriction": "Departure",
              "Status": "Close"
            }
		   ]
        }
      ]
    }
  }
}
```

> RESPOSTA (exemplo)

```json
{
  "RestrictionsRS": {
    "Success": ""
  }
}
```

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**RatePlanCode** <br>integer | ID do tipo de tarifa
**InvCode** <br>string | ID do tipo de quarto no Brasil Bookings
**Start** <br>string | Data de início do período
**End** <br>string | Data final do período
**Time** <br>integer | Quantidade de dias que deve se aplicar estadia mínima
**TimeUnit** <br>string | Tipo de unidade de tempo <br> **Valores possíveis:** `Day`
**MinMaxMessageType** <br>string | Tipo de restrição <br> **Valores possíveis:** `MinLOS`
**Restriction** <br>string | Tipo de bloqueio <br> **Valores possíveis:** `Arrival`, `Departure`
**Status** <br>string | Status da restrição <br> **Valores possíveis:** `Open`, `Close`

# Bloqueio/Desbloqueio de Tarifas

Através da rota `/block_rates_api/block_rates`, você pode bloquear ou desbloquear tarifas por período.

## Atualizando bloqueios/desbloqueios de tarifas

> POST https://app.brbookings.com/api/block_rates_api/block_rates (exemplo)

```json
{
  "BlockRateRQ": {
    "AvailStatusMessages": {
      "HotelCode": "1",
      "AvailStatusMessage": [
        {
          "StatusApplicationControl": {
            "Start": "2016-11-20",
            "End": "2016-11-21",
            "RatePlanCode": "1",
            "InvCode": "1"
          },
          "RestrictionStatus": { "Status": "Close" }
        },
        {
          "StatusApplicationControl": {
            "Start": "2016-11-21",
            "End": "2016-11-22",
            "RatePlanCode": "1",
            "InvCode": "1"
          },
          "RestrictionStatus": { "Status": "Open" }
        }
      ]
    }
  }
}
```

> RESPOSTA (exemplo)

```json
{
  "BlockRateRS": {
    "Success": ""
  }
}
```

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**RatePlanCode** <br>integer | ID do tipo de tarifa
**InvCode** <br>string | ID do tipo de quarto no Brasil Bookings
**Start** <br>string | Data de início do período
**End** <br>string | Data final do período
**Status** <br>string | Status da restrição <br> **Valores possíveis:** `Open`, `Close`


# Reservas

Através da rota `/reservations_api/reservations`, retornar as reservas feitas no Brasil Bookings.

## Baixa de Reservas

> GET https://app.brbookings.com/api/reservations_api/reservations

```json

```

> RESPOSTA (exemplo)

```json
{
  "ReservationRS": {
    "Reservations": [
      {
        "Channel": "3",
        "CreatedOn": "2015-10-13T00:00:00Z",
        "Status": "new",
        "ReserveId": "2",
        "Comments": "",
        "PaymentMethod": "CC",
        "TotalValue": "1099.00",
        "Currency": "USD",
        "Customer": {
          "CustomerFirstName": "Héloïse Kukasz",
          "CustomerMiddleName": "",
          "CustomerLastName": "Kukasz",
          "CustomerPhone": "",
          "CustomerEmail": ""
        },
        "Guests": [
          {
            "GuestResID": "142",
            "GuestName": "Héloïse Kukasz",
            "GuestMessage": ""
          },
          {
            "GuestResID": "144",
            "GuestName": "Camila Silva",
            "GuestMessage": ""
          }
        ],
        "Rooms": [
          {
            "RoomTypeId": "1",
            "CheckinDate": "2015-11-02",
            "CheckoutDate": "2015-11-09",
            "RoomTitle": "Nome do quarto",
            "Adults": 2,
            "Children": 0,
            "GuestIDs": [
              "142",
              "144"
            ],
            "DailyRates": [
              {
                "date": "2015-11-02",
                "totalValue": "157.00"
              },
              {
                "date": "2015-11-03",
                "totalValue": "157.00"
              },
              {
                "date": "2015-11-04",
                "totalValue": "157.00"
              },
              {
                "date": "2015-11-05",
                "totalValue": "157.00"
              },
              {
                "date": "2015-11-06",
                "totalValue": "157.00"
              },
              {
                "date": "2015-11-07",
                "totalValue": "157.00"
              },
              {
                "date": "2015-11-08",
                "totalValue": "157.00"
              }
            ]
          }
        ],
        "Payment": {
          "CardType": "CA",
          "CardNumber": "1234567890123456",
          "CardHolderName": "Despegar.com",
          "ExpireDate": "08/20"
        }
      }
    ]
  }
}
```

Propriedade | Descrição
-----------: | ---------
**Channel** <br>integer | ID do Canal onde a reserva foi feita <br> Veja na tabela de Canais, os valores possíveis
**CreatedOn** <br>string | Data da reserva
**Status** <br>string | Status da reserva <br> **Valores possíveis:** `new`, `modify`, `cancel`
**ReserveId** <br>string | ID da reserva
**Comments** <br>string | Comentários da reserva
**PaymentMethod** <br>string | Tipo de pagamento <br> Veja na tabela de Formas de Pagamento, os valores possíveis
**TotalValue** <br>float | Valor total da reserva
**Currency** <br>string | Moeda
**CustomerFirstName** <br>string | Primeiro nome do cliente
**CustomerMiddleName** <br>string | Nome do meio do cliente
**CustomerLastName** <br>string | Sobrenome do cliente
**CustomerPhone** <br>string | Telefone do cliente
**CustomerEmail** <br>string | E-mail do cliente
**GuestResID** <br>integer | ID do cliente dentro da reserva
**GuestName** <br>string | Nome completo do hóspede
**GuestMessage** <br>string | Mensagem do hóspede
**RoomTypeId** <br>integer | ID do tipo de quarto no Brasil Bookings
**CheckinDate** <br>string | Data de Checkin
**CheckoutDate** <br>string | Data do Checkout
**RoomTitle** <br>string | Nome do quarto
**Adults** <br>string | Quantidade de ocupantes do quarto
**Children** <br>integer | Quantidade de crianças no quarto
**GuestIDs** <br>integer | IDs dos hóspedes na reserva. Serve para identificar quais hóspedes estão em cada quarto.
**DailyRates - date** <br>string | Data da diária
**DailyRates - totalValue** <br>float | Valor da diária
**CardType** <br>string | Bandeira do cartão  de crédito <br> Veja na tabela de Bandeiras, os valores possíveis
**CardNumber** <br>string | Número do cartão de crédito
**CardHolderName** <br>string | Nome do titular do cartão de crédito
**ExpireDate** <br>string | Data de expiração do cartão de crédito

**CANAIS**

ID do Canal | Descrição
-----------: | ---------
**0** <br>integer | Brasil Bookings
**1** <br>integer | Booking.com
**3** <br>integer | Decolar.com

**STATUS**

Status | Descrição
-----------: | ---------
**all** | Todas as reservas
**new** | Reservas novas
**modify** | Reservas modificadas
**cancel** | Reservas canceladas

**FORMAS DE PAGAMENTO**

Status | Descrição
-----------: | ---------
**PP** | PayPal
**PPL** | PayPal Plus
**CC** | Cartão de Crédito
**DP** | Depósito
**BB** | BBPAY
**NA** | Não informado

**BANDEIRAS**

Status | Descrição
-----------: | ---------
**AX** | American Express
**BC** | Bank Card
**BL** | Card Bleu
**CB** | Carte Blanche
**DN** | Diners
**DS** | Discover Card
**EC** | Eurocard
**JC** | Japanese Credit Bureau Credit Card
**MA** | Maestro (Switch)
**MC** | Master Card
**TP** | Universal Air Travel Card
**VI** | Visa
**NA** | Não informado

<aside class="notice">
    Você pode baixar as reservas por status. Para isso você deve enviar a requisição como no exemplo abaixo: <br>
    <b>https://app.brbookings.com/api/reservations_api/reservations?status=all</b>
</aside>

## Confirmação da baixa de reservas

Após baixar uma reserva, você deve enviar um `POST` confirmando que efetuou a baixa da mesma em nosso sistema.

> POST https://app.brbookings.com/api/reservations_api/reservations (exemplo)

```json
{
  "ReservationRQ": {
    "Reservation": [
      {
        "HotelCode": "1",
        "ReserveId": "bo415874340"
      },
      {
        "HotelCode": "1",
        "ReserveId": "14504642041"
      }
    ]
  }
}
```

> RESPOSTA (exemplo)

```json
{
  "ReservationRS": {
    "Reservations": [
      {
        "ReserveId": "bo415874340",
        "HotelCode": "1",
        "Success": ""
      },
      {
        "ReserveId": "14504642041",
        "HotelCode": "1",
        "Success": ""
      }
    ]
  }
}
```

Propriedade | Descrição
-----------: | ---------
**HotelCode** <br>string | Código do hotel no Brasil Bookings
**ReserveId** <br>integer | ID da reserva
**Success** <br>string | Indica que a baixa da reserva foi concluída com sucesso



