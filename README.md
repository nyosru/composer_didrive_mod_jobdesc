# composer_didrive_mod_job_load_time_expectation
работа с загрузкой и обработкой времени ожидания


------- удаление кешей в аяксе (разобраться что такое) атрибут у ссылки  -------------

        cash_delete1_1="hoursonjob"
        cash_delete1_2name="date"
        cash_delete1_2="{{ date }}"
        cash_delete1_3name="sp"
        cash_delete1_3="{{ sp_now }}"





-------- блокировочный экран JS ----------
    $("body").append("<div id='body_block' class='body_block' >пару секунд вычисляем<br/><span id='body_block_465'></span></div>");

----- перезагрузка и блок -----
    location.reload();
    $("body").append("<div id='body_block' class='body_block' >пару секунд вычисляем<br/><span id='body_block_465'></span></div>");


храним ключи в мемкеш
dolgnosti - [ 'data' => [ dolgnosti ], 'sort' => [ dolg отсортированные по полю сортировки ] ]
в twig функции > jobdesc__get_dolgnosti



после любого действия с графиком .. трём кеш 
-------- php ---------
    // удаляем запись кеша главного массива данных
    if (!empty($_REQUEST['delete_cash_start_date'])) {
        $e = \f\Cash::deleteKeyPoFilter(['all', 'jobdesc', 'date' . date('Y-m-01',strtotime($_REQUEST['delete_cash_start_date'])) ]);
        // \f\pa($e);
    }



работа с кешем

        // если нет переменной то не пишем кеш            
        // если есть то показываем и считает время и память
        $show_timer = rand(0, 9999);

        if (!empty($show_timer)) {
            \f\timer_start($timer_rand);
            $cash_var = 'jobdesc__money_minus_mod' . self::$mod_minus . '_datestart' . $date_start . '_datefinish' . $date_finish;
            $cash_time_sec = 0;
        }

        $return = [];

        if (!empty($show_timer)) {
            echo '<br/>#' . __LINE__ . ' var ' . $cash_var;
            $return = \f\Cash::getVar($cash_var);
        }

        if (!empty($return)) {
            if (!empty($show_timer))
                echo '<br/>#' . __LINE__ . ' данные из кеша';
        } else {

            if (!empty($show_timer))
                echo '<br/>#' . __LINE__ . ' считаем данные и пишем в кеш';

            // тут супер код делающий $return старт

            // тут супер код делающий $return конец

            if (!empty($return))
                \f\Cash::setVar($cash_var, $return, ( $cash_time_sec ?? 0));
        }

        if (!empty($show_timer))
            echo '<br/>#'.__LINE__.' '.\f\timer_stop ($show_timer);
