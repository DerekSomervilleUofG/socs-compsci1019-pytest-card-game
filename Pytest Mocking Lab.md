# Pytest Mocking Lab

This lab introduces core `pytest` concepts, including the `mocker` fixture, `monkeypatch`, exception handling, and parametrization. 

## Sub-task 1 – Mock External API Response (Return Value)

To mock a network request and control the JSON response returned to the application.

**Requirement**

Implement unit test `test_fetch_player_stats` in `test/test_mock_Network.py` to mock an external API call.

1. We want to test `NetworkUtils.fetch_player_stats` which calls `requests.get` to retrieve a player's profile from a server.
2. Mock `requests.get` using pytest's `mocker.patch` so that it returns a mock response object. Configure this mock object so its `.json()` method returns `{"wins": 10, "losses": 2, "rank": "Gold"}`.
3. Call `fetch_player_stats` with any player ID.
4. The expected output of the unit test, namely the value returned by the function, should be the parsed dictionary. Assert that the `rank` key in the returned dictionary equals `"Gold"`.

*Push sub task to GitHub, Go To GitHub Commit*

---

## Sub-task 2 – Simulate an Exception (Side Effects)

To mock a database function to raise an error and verify the application's exception handling using pytest.

**Requirement**

Implement unit test `test_save_score_connection_error` in `test/test_mock_Database.py` to simulate a system failure.

1. We want to test `Database.save_score`, which calls `db_connector.execute` to save the game results. If the database fails, it is supposed to raise a custom `DatabaseConnectionError`.
2. Mock `db_connector.execute` and set its `side_effect` to raise a standard Python `ConnectionError`.
3. Use the `pytest.raises(DatabaseConnectionError)` context manager.
4. Call `save_score` with a valid score. Verify that the test passes, meaning your mocked `ConnectionError` was successfully caught and re-raised as the custom `DatabaseConnectionError` by the application.

*Push sub task to GitHub, Go To GitHub Commit*

---

## Sub-task 3 – Alter Environment Variables using Monkeypatch

To safely mock environment variables during a test without permanently altering the system.

**Requirement**

Implement unit test `test_get_server_url_production` in `test/test_mock_Config.py` to test configuration loading.

1. We want to test `Config.get_server_url`, which reads the `GAME_ENV` system environment variable using `os.getenv` to determine which server URL to return. 
2. Use pytest's built-in `monkeypatch` fixture to set the `GAME_ENV` environment variable to `production` using `monkeypatch.setenv("GAME_ENV", "production")`.
3. The expected output of the unit test, namely the value returned by `Config.get_server_url`, should be `"https://api.mycardgame.com"`.
4. Assert that the returned string exactly matches the expected production URL. 

*Push sub task to GitHub, Go To GitHub Commit*

---

## Sub-task 4 – Parametrized Tests with Mocks

To run a single mocked test multiple times against different inputs using pytest parametrization.

**Requirement**

Implement unit test `test_calculate_damage_critical` in `test/test_mock_Combat.py` to verify combat math across different weapon types.

1. We want to test `Combat.calculate_damage(base_damage)`, which calls `random.uniform(1.0, 2.0)` to apply a random critical hit multiplier to a weapon's base damage. 
2. Decorate your test function with `@pytest.mark.parametrize` to pass in three different `base_damage` inputs: `10`, `20`, and `50`.
3. Mock `random.uniform` in `card_game.combat.Combat` to always return exactly `1.5`.
4. Call `calculate_damage(base_damage)` for each parametrized input. 
5. Assert that the returned values are `15`, `30`, and `75`, respectively, verifying that the fixed mocked multiplier is applied correctly to all test cases.

*Push sub task to GitHub, Go To GitHub Commit*

---

## Sub-task 5 – Mock Date and Time (Patching Modules)

To fix the system clock to a specific date to test time-based conditional logic.

**Requirement**

Implement unit test `test_get_daily_bonus_weekend` in `test/test_mock_Rewards.py` to mock the system date.

1. We want to test `Rewards.get_daily_bonus`, which calls `datetime.date.today()` to check the current day of the week. If it is a weekend, the bonus should be `200`; otherwise, it is `100`.
2. Mock `datetime.date` inside the `card_game.rewards.Rewards` module to return a specific mock date representing a Saturday (e.g., `datetime.date(2026, 11, 7)`).
3. Call `get_daily_bonus()`.
4. The expected output of the unit test, namely the value returned by the function, should be `200`.
5. Verify that `today()` was called exactly once on your mocked date object.

*Push sub task to GitHub, Go To GitHub Commit*