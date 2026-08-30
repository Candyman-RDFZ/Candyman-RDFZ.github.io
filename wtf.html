#include <iostream>
#include <random>
#include <cstdint>
#include <cmath>
#include <algorithm>

using namespace std;

typedef unsigned long long ull;
typedef __uint128_t u128;

const ull LIM = 1000000000000000000ULL;
const ull HALF = 500000000000000000ULL;
const ull QTR = 250000000000000000ULL;
const ull THREE_QTR = 750000000000000000ULL;

const double NEG_INF = -1e100;

// ------------------------------------------------------------
// Basic utilities
// ------------------------------------------------------------

ull gcd_ull(ull a, ull b) {
    while (b != 0) {
        ull t = a % b;
        a = b;
        b = t;
    }
    return a;
}

ull abs_diff(ull a, ull b) {
    if (a >= b) return a - b;
    return b - a;
}

bool is_power_of_two(ull x) {
    return x != 0 && (x & (x - 1)) == 0;
}

// ------------------------------------------------------------
// Miller-Rabin
// Deterministic for 64-bit integers with these bases.
// ------------------------------------------------------------

ull mul_mod(ull a, ull b, ull mod) {
    return (ull)((u128)a * b % mod);
}

ull pow_mod(ull a, ull e, ull mod) {
    ull result = 1;

    while (e) {
        if (e & 1ULL)
            result = mul_mod(result, a, mod);

        a = mul_mod(a, a, mod);
        e >>= 1;
    }

    return result;
}

bool is_prime(ull n) {
    if (n < 2)
        return false;

    static const ull small_primes[] = {
        2ULL, 3ULL, 5ULL, 7ULL, 11ULL, 13ULL,
        17ULL, 19ULL, 23ULL, 29ULL, 31ULL, 37ULL
    };

    for (int i = 0; i < 12; ++i) {
        ull p = small_primes[i];

        if (n % p == 0)
            return n == p;
    }

    ull d = n - 1;
    int s = 0;

    while ((d & 1ULL) == 0) {
        d >>= 1;
        ++s;
    }

    static const ull bases[] = {
        2ULL,
        325ULL,
        9375ULL,
        28178ULL,
        450775ULL,
        9780504ULL,
        1795265022ULL
    };

    for (int i = 0; i < 7; ++i) {
        ull a = bases[i];

        if (a % n == 0)
            continue;

        ull x = pow_mod(a % n, d, n);

        if (x == 1 || x == n - 1)
            continue;

        bool ok = false;

        for (int r = 1; r < s; ++r) {
            x = mul_mod(x, x, n);

            if (x == n - 1) {
                ok = true;
                break;
            }
        }

        if (!ok)
            return false;
    }

    return true;
}

// ------------------------------------------------------------
// c = 3 detector
// ------------------------------------------------------------

struct SeedState {
    mt19937_64 rng;
    uniform_int_distribution<ull> dist;
    bool alive;

    SeedState() : rng(1), dist(0ULL, LIM), alive(true) {}

    void init(ull seed) {
        rng.seed(seed);
        alive = true;
    }

    ull next() {
        return dist(rng);
    }
};

// ------------------------------------------------------------
// Main
// ------------------------------------------------------------

int main() {
    ios::sync_with_stdio(false);
    cin.tie(nullptr);

    int n;
    ull a;

    cin >> n >> a;

    // --------------------------------------------------------
    // c = 2
    //
    // A permutation of 1..n.
    // --------------------------------------------------------

    bool *used = new bool[n + 1];

    for (int i = 0; i <= n; ++i)
        used[i] = false;

    bool permutation_possible = true;

    if (a < 1 || a > (ull)n) {
        permutation_possible = false;
    } else {
        used[(int)a] = true;
    }

    // --------------------------------------------------------
    // c = 3
    //
    // Try all five possible seeds.
    // --------------------------------------------------------

    SeedState seed[5];

    for (int i = 0; i < 5; ++i)
        seed[i].init((ull)(i + 1));

    for (int i = 0; i < 5; ++i) {
        if (seed[i].next() != a)
            seed[i].alive = false;
    }

    // --------------------------------------------------------
    // c = 1
    //
    // All differences must be multiples of 2^k.
    //
    // Maintain:
    //
    // g = gcd(|a_i-a_1|)
    // --------------------------------------------------------

    ull g = 0;

    // --------------------------------------------------------
    // c = 4
    //
    // Every element must be composite.
    // --------------------------------------------------------

    bool composite_possible = true;

    if (a < 2 || is_prime(a))
        composite_possible = false;

    // --------------------------------------------------------
    // c = 5,6,7
    //
    // These have identical feature vectors, so we only need
    // to determine whether at least one remains possible.
    // --------------------------------------------------------

    bool possible5 = true;
    bool possible6 = true;
    bool possible7 = true;

    if (a > HALF)
        possible5 = false;

    if (a < HALF)
        possible6 = false;

    if (a < QTR || a > THREE_QTR)
        possible7 = false;

    // --------------------------------------------------------
    // c = 8,9
    //
    // Identical feature vectors.
    // --------------------------------------------------------

    bool special_found = (a == 0 || a == 1);

    // --------------------------------------------------------
    // Evidence scores
    //
    // These are deliberately conservative. We don't want
    // to commit to a special class from weak evidence.
    // --------------------------------------------------------

    double order_score = 0.0;
    double seed_score = 0.0;
    double composite_score = 0.0;
    double range_score = 0.0;
    double special_score = 0.0;
    double random_score = 0.0;

    if (special_found) {
        special_score = 1000.0;
    } else {
        special_score = -0.5;
    }

    if (composite_possible)
        composite_score = 0.05;
    else
        composite_score = NEG_INF;

    // --------------------------------------------------------
    // Prediction function
    // --------------------------------------------------------

    auto choose_prediction = [&]() -> int {
        // c = 8 / 9
        if (special_found)
            return 8;

        // Count surviving seeds.
        int alive_seeds = 0;

        for (int i = 0; i < 5; ++i) {
            if (seed[i].alive)
                ++alive_seeds;
        }

        double s_seed;

        if (alive_seeds == 0) {
            s_seed = NEG_INF;
        } else {
            /*
             * Exact prefix agreement with one of the five
             * generators is extraordinarily strong evidence.
             */
            s_seed = seed_score + 50.0 * alive_seeds;
        }

        // ----------------------------------------------------
        // ORDER = c=1 or c=2
        // ----------------------------------------------------

        double s_order = order_score;

        if (!permutation_possible)
            s_order -= 0.5;

        if (g != 0) {
            if (is_power_of_two(g)) {
                s_order += 5.0;
            } else {
                /*
                 * Remove all powers of two from g.
                 * If something remains, g has an odd factor.
                 */
                ull x = g;

                while ((x & 1ULL) == 0)
                    x >>= 1;

                if (x == 1)
                    s_order += 3.0;
                else
                    s_order -= 1.0;
            }
        }

        // ----------------------------------------------------
        // RANGE = c=5/6/7
        // ----------------------------------------------------

        double s_range;

        if (possible5 || possible6 || possible7)
            s_range = range_score;
        else
            s_range = NEG_INF;

        // ----------------------------------------------------
        // COMPOSITE = c=4
        // ----------------------------------------------------

        double s_composite = composite_possible
                           ? composite_score
                           : NEG_INF;

        // ----------------------------------------------------
        // Find maximum.
        // ----------------------------------------------------

        double best = random_score;
        int answer = 10;

        if (s_order > best) {
            best = s_order;
            answer = 1;
        }

        if (s_seed > best) {
            best = s_seed;
            answer = 3;
        }

        if (s_composite > best) {
            best = s_composite;
            answer = 4;
        }

        if (s_range > best) {
            best = s_range;
            answer = 5;
        }

        if (special_score > best) {
            best = special_score;
            answer = 8;
        }

        return answer;
    };

    // --------------------------------------------------------
    // FIRST PREDICTION
    //
    // Must happen before reading a2.
    // --------------------------------------------------------

    cout << choose_prediction() << endl;

    // --------------------------------------------------------
    // Remaining n-1 rounds
    // --------------------------------------------------------

    for (int i = 2; i <= n; ++i) {
        ull x;
        cin >> x;

        // ----------------------------------------------------
        // c = 3
        // ----------------------------------------------------

        for (int s = 0; s < 5; ++s) {
            if (!seed[s].alive)
                continue;

            ull expected = seed[s].next();

            if (expected != x)
                seed[s].alive = false;
        }

        // ----------------------------------------------------
        // c = 2
        // ----------------------------------------------------

        if (permutation_possible) {
            if (x < 1 || x > (ull)n) {
                permutation_possible = false;
            } else {
                int v = (int)x;

                if (used[v]) {
                    permutation_possible = false;
                } else {
                    used[v] = true;
                }
            }
        }

        // ----------------------------------------------------
        // c = 1
        // ----------------------------------------------------

        ull d = abs_diff(x, a1);

        if (g == 0)
            g = d;
        else
            g = gcd_ull(g, d);

        // ----------------------------------------------------
        // c = 4
        // ----------------------------------------------------

        if (composite_possible) {
            if (x < 2 || is_prime(x)) {
                composite_possible = false;
                composite_score = NEG_INF;
            } else {
                /*
                 * Being composite is weak evidence because
                 * random numbers are also usually composite.
                 */
                composite_score += 0.05;
            }
        }

        // ----------------------------------------------------
        // c = 5
        // ----------------------------------------------------

        if (x > HALF)
            possible5 = false;

        // ----------------------------------------------------
        // c = 6
        // ----------------------------------------------------

        if (x < HALF)
            possible6 = false;

        // ----------------------------------------------------
        // c = 7
        // ----------------------------------------------------

        if (x < QTR || x > THREE_QTR)
            possible7 = false;

        // Give a small amount of evidence while at least one
        // of the three range classes is still possible.
        if (possible5 || possible6 || possible7)
            range_score += 0.03;
        else
            range_score = NEG_INF;

        // ----------------------------------------------------
        // c = 8 / 9
        // ----------------------------------------------------

        if (x == 0 || x == 1) {
            special_found = true;
            special_score = 1000.0;
        }

        // ----------------------------------------------------
        // c = 1 evidence
        // ----------------------------------------------------

        if (g != 0) {
            if (is_power_of_two(g)) {
                order_score += 0.8;
            } else {
                ull t = g;

                while ((t & 1ULL) == 0)
                    t >>= 1;

                if (t == 1)
                    order_score += 0.4;
                else
                    order_score -= 0.2;
            }
        }

        // ----------------------------------------------------
        // c = 2 evidence
        // ----------------------------------------------------

        if (permutation_possible)
            order_score += 0.02;
        else
            order_score -= 0.02;

        // ----------------------------------------------------
        // c = 3
        // ----------------------------------------------------

        int alive_seeds = 0;

        for (int s = 0; s < 5; ++s) {
            if (seed[s].alive)
                ++alive_seeds;
        }

        if (alive_seeds == 0) {
            seed_score = NEG_INF;
        } else {
            seed_score += 0.5;
        }

        // ----------------------------------------------------
        // OUTPUT CURRENT PREDICTION
        //
        // This MUST happen before the next cin.
        // endl flushes stdout.
        // ----------------------------------------------------

        cout << choose_prediction() << endl;
    }

    delete[] used;

    return 0;
}
