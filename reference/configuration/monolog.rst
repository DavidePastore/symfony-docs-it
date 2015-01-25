.. index::
   pair: Monolog; Riferimento configurazione

Riferimento configurazione
==========================

Configurazione predefinita completa
-----------------------------------

.. configuration-block::

    .. code-block:: yaml

        monolog:
            handlers:

                # Esempi:
                syslog:
                    type:                stream
                    path:                /var/log/symfony.log
                    level:               ERROR
                    bubble:              false
                    formatter:           mio_formattatore
                main:
                    type:                fingers_crossed
                    action_level:        WARNING
                    buffer_size:         30
                    handler:             custom
                console:
                    type:                console
                    verbosity_levels:
                        VERBOSITY_NORMAL:       WARNING
                        VERBOSITY_VERBOSE:      NOTICE
                        VERBOSITY_VERY_VERBOSE: INFO
                        VERBOSITY_DEBUG:        DEBUG
                custom:
                    type:                service
                    id:                  my_handler

                # Opzioni e valori predefiniti per un "mio_gestore"
                # Nota: molte di queste opzioni dipendono da "type".
                # Per esempio, il tipo "service" non usa alcuna opzione,
                # tranne id e channels
                mio_gestore:
                    type:                 ~ # Obbligatorio
                    id:                   ~
                    priority:             0
                    level:                DEBUG
                    bubble:               true
                    path:                 "%kernel.logs_dir%/%kernel.environment%.log"
                    ident:                false
                    facility:             user
                    max_files:            0
                    action_level:         WARNING
                    activation_strategy:  ~
                    stop_buffering:       true
                    buffer_size:          0
                    handler:              ~
                    members:              []
                    channels:
                        type:     ~
                        elements: ~
                    from_email:           ~
                    to_email:             ~
                    subject:              ~
                    mailer:               ~
                    email_prototype:
                        id:                   ~ # Obbligatorio (se si usa email_prototype)
                        method:               ~
                    formatter:            ~

    .. code-block:: xml

        <container xmlns="http://symfony.com/schema/dic/services"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xmlns:monolog="http://symfony.com/schema/dic/monolog"
            xsi:schemaLocation="http://symfony.com/schema/dic/services http://symfony.com/schema/dic/services/services-1.0.xsd
                                http://symfony.com/schema/dic/monolog http://symfony.com/schema/dic/monolog/monolog-1.0.xsd">

            <monolog:config>
                <monolog:handler
                    name="syslog"
                    type="stream"
                    path="/var/log/symfony.log"
                    level="error"
                    bubble="false"
                    formatter="my_formatter"
                />
                <monolog:handler
                    name="main"
                    type="fingers_crossed"
                    action-level="warning"
                    handler="custom"
                />
                <monolog:handler
                    name="console"
                    type="console"
                />
                <monolog:handler
                    name="custom"
                    type="service"
                    id="my_handler"
                />
            </monolog:config>
        </container>

.. note::

    Quando il profilatore è abilitato, viene aggiunto un gestore per memorizzare i messaggi
    di log nel profilatore. Il profilatore usa il nome "debug", quindi il nome è riservato e
    non può essere usato nella configurazione.
