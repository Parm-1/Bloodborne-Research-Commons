# RTC calendar admission, conversion and local formatting

**Status — 2026-10-17:** proposed SOURCE_INSPECTED BRC-RTC-CONVERSION-01, Batch04 [Issue #24](https://github.com/Parm-1/Bloodborne-Research-Commons/issues/24), one goal/one PR. Independent source [review r1](../docs/reviews/BRC-RTC-CONVERSION-01-REVIEW-r1.md) is complete with no actionable finding at `a2007ccfe20c286065a12caaab05cf0d3fd948c3`, tree `86dec37f90b11e38308f95ba31ca61c4b6bf3ec7`. Root accepts the conditional SOURCE_INSPECTED contract for one unmerged reference/editorial PR only; owner editorial acceptance/merge pending. No candidate repair or affected recheck required. [Final author integration r2](../docs/reviews/BRC-RTC-CONVERSION-01-AUTHOR-r2.md). [RC-0048](../claims/RC-0048-rtc-calendar-range.md), [RC-0049](../claims/RC-0049-rtc-local-result.md), [frontier](../frontiers/rtc-conversion.md), [author r1](../docs/reviews/BRC-RTC-CONVERSION-01-AUTHOR-r1.md). Reviewed/unmerged probe-image PR #32 over rwlock #31 over eventqueue #30 is an integration-only predecessor, not corroboration. Owner editorial acceptance/merge remain pending. Incorporated main `689e2e29ed67d1c4f5231a1254b93ffd88586bc8` and first five Batch04 incorporations remain unchanged.

Consumer: a calendar API maintainer deciding which date/tick/Unix-seconds pair may round-trip and what a local conversion or formatting return establishes. **Retain the entry route, raw field widths, admitted range, UTC/local interpretation and host success premises. Validate a date separately from admitting a raw tick; require the caller's output capacity.** This reference does not change implementation or qualify a target.

## Exact source and separate descriptions

Public [deadinside28/bloodborne_pc](https://github.com/deadinside28/bloodborne_pc), supplied commit `3c57da4198ad62039f63f33bfd205b9916518acf`, tree `ab584d54c478824a75bef51a3f5fe349e5a3c415`. Selected Linux x86-64 source; no new upstream freshness query. Full blobs identify files; selected bounds identify inspected text.

| Path at the pin | Selected bounds | Full blob | Role |
|---|---|---|---|
| [src/runtime_rtc.c][rtc] | 1–151, complete | `055b037cbbf856abe4ef83f476af69adacd125b3` | date producer, admission, conversions, formatter and exports |
| [src/runtime.c][runtime] | 70–85, 204–261, 263–282 | `0f8a947a52f384668097055c6dbfe432c79a4de8` | capability and exact scoped lookup; reused bounded import route |
| [src/runtime.h][header] | 1–17, 54–58, 93 | `3d8cf3c379642f47043a6fe28741116678a2e414` | ABI annotation and declarations |
| [src/import_names.inc][names] | 286, 309–311, 584, 587–588, 625, 658–659; complete selected-name search | `55e92852fc94db7445614329c44f38377b24e715` | ten selected scoped mappings, three selected export absences |
| [src/probe.c][probe] | 528–542 | `75ead5c8ffd6955891e88c9741134c47059fc825` | address installation, not invocation |
| [gpu/shim/bbgpu.cpp][shim] | 305–321 | `d71cfc41a9e532ff1c0e30ccc9073d24726315d3` | distinct prefix fallback limit |
| [gpu/bbnet/include/core/libraries/rtc/rtc.h][netheader] | 1–44, 46–82 | `06832cc4daf1ffaa8d7eb4e492feb3bcb5aa5c75` | separate GPL header declarations, not an independent implementation/ABI observation |
| [build.sh][build] | 1–23, 73–82, read only | `9b7b7c96a1ef8d7b31d2a9e8d8067bb9f4fcf042` | runtime glob and C11 build declaration |
| [README.md][readme] | 394–402, reused license receipt | `b7004d7901749ab08dd296ac4f198c230ca19dda` | GPL v2-or-later declaration |
| [LICENSE][license] | 1–8, reused receipt | `9efa6fbc962836e243e20f7f23db062e2c077d28` | GPL v2 text |
| [gpu/VENDOR.txt][vendor] | 1–5, reused receipt | `4a8603c7854cfb254ae105f8f21b34d36a6cf102` | lineage/dependency limits |

Separately read 2026-10-17: primary Linux man-pages [clock_gettime/getres](https://man7.org/linux/man-pages/man3/clock_gettime.3.html), [localtime_r and related conversions](https://man7.org/linux/man-pages/man3/localtime.3.html), [struct tm](https://man7.org/linux/man-pages/man3/tm.3type.html), [snprintf](https://man7.org/linux/man-pages/man3/snprintf.3.html); [GCC x86 attributes](https://gcc.gnu.org/onlinedocs/gcc/x86-Attributes.html), sysv_abi; [WG14 N1570](https://www.open-std.org/jtc1/sc22/wg14/www/docs/n1570.pdf), C11 draft2011-04-12, §§6.2.5p9, 6.3.1.1/3, 6.5p5, 6.5.5p6, 6.7.9p10, 7.21.6.1/5, 7.24.2.1. Six substantive descriptions, separate from implementation evidence. Clock page identifies release5.07/rendering2020-07-14; the other three man pages identify6.19/rendering2026-09-09. The attempted GCC x86-Function-Attributes URL supplied no substantive contract; the x86-Attributes page did. Mutable documentation bytes are not frozen. No installed compiler, libc/time_t/struct layout, timezone database, kernel or console ABI is qualified.

## Callable route and storage identity

[Resolver:204–261,263–278][runtime] requires capability bit0 and a function request. RTC dispatch follows pad and precedes savedata/file; exact lookup first maps a complete scoped NID to a readable symbol, then finds that symbol in [exports:143–151][rtc]. A plain symbol string is insufficient. Reuse the [import study](import-resolution.md) for the surrounding mechanism, not a full resolver reaudit. [Probe:528–542][probe] installs resolved address plus addend; that is no invocation receipt.

| Exact table NID | RTC export selected |
|---|---|
| `zO9UL3qIINQ#H#I` | GetCurrentNetworkTick |
| `bDEVVP4bTjQ#H#I` | SetTime_t |
| `8w-H19ip48I#H#I` | GetTick |
| `jMNwqYr4R-k#H#I` | GetTickResolution |
| `ZPD1YOKI+Kw#H#I` | GetCurrentClockLocalTime |
| `M1TvFst-jrM#H#I` | ConvertUtcToLocalTime |
| `8Yr143yEnRo#H#I` | ConvertLocalTimeToUtc |
| `AxHBk3eat04#H#I` | FormatRFC2822LocalTime |
| `ueega6v3GUw#H#I` | SetTick |
| `CyIK-i4XdgQ#H#I` | GetDayOfWeek |

All names above have `sceRtc` prefix. Complete selected-symbol search of the table finds no mapping for `sceRtcGetCurrentTick`, `sceRtcGetCurrentClock` or `sceRtcGetTime_t`, despite their exports. Their bodies remain inspectable; do not represent them as selected through this table. The final GPU fallback matches registered NID prefixes [shim:313–321][shim]; table absence alone is not global unreachability. No matching fallback registration/invocation is established here.

`DateTime` declares six uint16 fields year/month/day/hour/minute/second and one uint32 microsecond, with a sizeof16 static assertion [21–22][rtc]. Ticks are uint64; SetTime_t takes int64 seconds; GetTime_t writes int64. Wrappers use `sysv_abi` [header:13][header]. The separate bbnet header declares a one-u64 tick struct and corresponding fields but uses native `time_t` for its Unix interfaces; it does not establish compiled compatibility with these int64 functions, actual offsets/alignment/endianness, original-console prototypes or reachability. GCC describes the intended System V calling convention, not a compiled ABI test.

Caller-owned inputs must remain readable, typed/aligned and stable through all reads; outputs must be writable for the actual size throughout the call. Use distinct nonoverlapping date/tick/output storage for the conditional cases. Null checks do not establish mapping, capacity, ownership or race freedom. No pointer is retained by the selected RTC bodies; stack `tm`, `DateTime` and text intermediates are consumed synchronously, and formatted bytes are copied into caller storage, not returned as a borrowed stack pointer. Plain multi-field writes are not atomic snapshots or transactional publication. Concurrent conflicting access, faults or nonlocal exits fall outside defined normal-return claims.

A bounded search of public src/tests/scripts/gpu/shim for these selected names/NIDs finds the declarations/exports/name mappings and the formatter's internal day-of-week call, but no separate selected public test or application invocation. Broader name search also found the separate bbnet declaration header above, not an observed caller. No global absence or original-game inference follows. Actual caller arguments/order, loaded address and host artifact remain UNKNOWN.

## Date admission and raw tick arithmetic

[Validation:24–64,103–112][rtc] admits year1..9999, month1..12, day1..days-in-month under Gregorian leap rule, hour0..23, minute/second0..59 and microsecond0..999999. Leap seconds60 are rejected. Validation order is year, month, day, hour, minute, second, microsecond, so invalid month stops before indexing days-in-month. GetTick first rejects either null pointer, validates, then writes only on success. DayOfWeek independently checks year/month/day and returns `(days+1)%7` (Sunday0, Monday1), not an error/status pair.

Let D=86,400,000,000 microseconds/day and E=`0xdcbffeff2bc000`=62,135,596,800,000,000. `to_tick` computes Gregorian days from0001-01-01 timesD, then whole seconds times1,000,000 plus microseconds. For admitted dates the arithmetic fits uint64: the greatest tick is315,537,897,599,999,999 at9999-12-31 23:59:59.999999;10000-01-01 starts315,537,897,600,000,000. E corresponds to719,162 days to1970-01-01. These are static integer derivations, not calendar-library outputs or observations of another RTC.

SetTick only checks pointers and calls `from_tick`; it performs no admitted-year check. `from_tick` splits unsigned tick/D and tick%D, derives civil fields, and casts the computed year to uint16. Under the selected intended int32-or-wider arithmetic, raw uint64 spans more than the admitted calendar range. Year10000 is representable in uint16 but invalid to GetTick. Year65537 narrows to1, losing whole eras even though the resulting fields can pass validation. Thus the bounded date→tick→date and tick→date→tick correspondence for the admitted year1..9999 domain must not be extended to every raw tick accepted with return0. The ordinary civil formulas and worked endpoints support this source contract; no exhaustive algorithm correctness or target-fidelity proof is supplied.

[Unix conversion:114–125][rtc]: SetTime_t rejects null output, then seconds<0 with raw32 `0x80B50003`, and otherwise passes `(E + uint64(seconds)*1,000,000) mod2^64` to from_tick. No positive upper-bound or resulting-year validation occurs. Positive signed64 input can wrap during unsigned scaling/addition. GetTime_t checks both pointers and validates the date; it writes0 for any tick<E, otherwise floor((tick-E)/1,000,000). It loses fractional microseconds and collapses all admitted pre-1970 dates to0, rather than returning negative Unix seconds. Its maximum admitted result is253,402,300,799. Whole seconds from0 through that bound can correspond to admitted dates; this conditional inverse does not extend to subsecond fields, pre-epoch dates or unbounded positive SetTime_t inputs. GetTime_t's table-selection absence remains separate from its body semantics.

Unsigned wrap/narrowing follows N1570's unsigned rules. By contrast, uint64→int64 values above INT64_MAX have implementation-defined conversion or signal, and signed arithmetic overflow is undefined. Do not silently treat every signed path as two's-complement modular arithmetic. Error macros also use int32 casts of high-bit hex constants; report their raw32 intent without claiming an installed signed result representation.

## Host now and UTC/local phases

[65–96][rtc]: now_utc calls host CLOCK_REALTIME into an uninitialized automatic timespec, ignores its result, then forms `(E + uint64(tv_sec)*1,000,000 + uint64(tv_nsec)/1000) mod2^64`. With a successful normalized nonnegative sample in range this translates wall Epoch seconds and truncates nanoseconds to microseconds. It is not monotonic, a clock accuracy measurement or a guaranteed fresh/increasing sample. `GetTickResolution` returns the constant1,000,000; this declares scale, not a measured host resolution/precision or synchronization. GetCurrentNetworkTick and GetCurrentTick share the exact same function pointer; no networking or independent network clock is implemented here. Separate invocations are separate samples. Reuse [clock/sleep scope](clock-sleep.md) for other clocks; do not import its reviewed status as RTC corroboration.

CurrentClock adds caller int32 minutes*60,000,000 to a signed-cast now tick before conversion. All int32 minute products fit int64, but the signed sum still requires representability. No timezone-range check exists. CurrentClockLocalTime obtains one UTC sample, obtains that sample's host local offset, then converts the sum. These paths do not call date validation or propagate host errors.

`local_offset(u)` first computes **unsigned** u-E, casts to int64, divides by1,000,000 with truncation toward zero, casts to native time_t, calls localtime_r unchecked and multiplies tm_gmtoff by1,000,000. The Linux description defines tm_gmtoff as seconds east of UTC; successful localtime_r writes caller-supplied tm using host timezone rules. A valid interpreted time_t, initialized offset and representable multiplication are premises. For u<E, unsigned subtraction underflows before the signed cast: the source supplies no portable negative-time conversion. Even under a separately qualified wrap-to-signed interpretation, E-1 yields trunc(-1/1,000,000)=0, not floor=-1. Native time_t range and host historical timezone behavior are not inferred from the source.

Write O(u) for a successfully obtained representable offset at u. UTC→local calculates L=u+O(u); local→UTC calculates v=L-O(L), **looking up L as if it were UTC**. With representable signed casts/sums and a common stable timezone definition, v=u only if O(L)=O(u). This gives a useful constant-offset positive, not an inverse across every transition. No local civil-time solving, mktime, ambiguity flag, nonexistent-time detection or DST branch selection occurs. A local tick contains no timezone identity or fold selector. Changing timezone configuration between calls also defeats an assumed common O. Raw input/output units alone cannot establish UTC identity or a unique inverse.

CLOCK_REALTIME and localtime_r may fail under their separate host descriptions. Their status is ignored here; automatic samples/fields can remain indeterminate. Return0 on paths that reach it does not independently establish host success. No deterministic output, fault behavior or defined return after an indeterminate read is claimed. These RTC bodies do not adapt host errno into guest TLS errors; failure premises must be checked independently, not inferred from unrelated errno state.

## Selected formatter and result boundary

[126–140][rtc] rejects null out, uses a provided UTC tick or samples now when the tick pointer is null, obtains O(u), converts u+O(u), indexes fixed English weekday/month arrays, requests text in a local64-byte snprintf buffer, then memcpy(out,text,strlen(text)+1) and returns0. It never calls date validation before array indexing. DayOfWeek may return a negative error-intent result for a year outside1..9999; using that result as an array index is not a valid formatted-output path. Raw tick acceptance by SetTick therefore cannot authorize formatting that tick. Month must also support index month-1. Keep representable shifted tick, admitted calendar year/date, successful host/format operations and valid array indices as explicit premises.

The request is weekday, comma, two-digit day, English month, minimum-four-digit year, hh:mm:ss and signed hhmm from offset minutes. Microseconds are omitted; offset seconds are truncated toward zero to minutes. `%04u`/`%02u` are minimum widths, not range checks. For the intended admitted four-digit-year/two-digit-offset-hours rendering, text has31 bytes plus NUL, so caller needs32 writable bytes. The source comment says the SDK buffer size; that is PROJECT_REPORTED, not an independently read SDK contract. No destination length is supplied or checked;64 protects only the stack temporary. More generally destination capacity must cover actual strlen(text)+1 (at most64 only if the bounded formatting completed with valid NUL termination). Do not infer a safe31-byte destination from the comment.

Formatting calls also require the native promoted-argument/format contract: the uint16 fields undergo integer promotion but are supplied to `%u` conversions without explicit unsigned casts. On the usual int32 promotion those arguments have int type while `%u` specifies unsigned int; N1570 §7.21.6.1p9 does not provide a portable mismatched-type success guarantee. This study records the intended rendering and capacity calculation, not an unconditional strictly portable snprintf success or a demonstrated installed-host defect. It qualifies no native printf ABI. snprintf's return/truncation/error is ignored; a failed call is not a successful result receipt, and no initialized text/strlen safety is assumed after a failure.

Null/invalid-date/negative-seconds errors above occur before caller output writes in their selected functions. Successful conversion may write DateTime field by field; formatter's final copy has no checked capacity or rollback. No reported pointer fault, partial-copy state or host-failure output is invented. A successful source path means the synchronous operations completed under their premises, not that output was atomically published, retained by an owner, original-console compliant, RFC-conformant for every input, or consumed by a real game.

## Conditional source/model cases — zero executed

Each row uses the pinned control flow and independent scalar premises. Values are original reasoning examples, not produced fixture bytes, calendar/timezone oracle results, tests or pass counts. Date tuples are year-month-day followed by time/microsecond when needed. All storage is valid, separate and stable unless a missing premise is the point. Formatting positives describe the intended rendering subject to the native formatting qualification above.

| ID / phase | Source-faithful positive and contradictory fields | Supported distinction |
|---|---|---|
| A1 admission | GetTick date0001-01-01 00:00:00.000000 writes0; changing raw year to0 or10000 returns year error before write | earliest field and lower/upper admission, not raw tick validity |
| A2 leap/day | 2000-02-29 is admitted (divisible400);1900-02-29 returns day error (divisible100, not400);1900-02-28 admitted | actual leap rule, not every divisible4 year |
| A3 validation order | year2026/month1/day1 admitted; month13/day0 returns month error before day lookup; year0/month13 returns year error | competing invalid fields cannot replace ordered checks |
| A4 subday fields | 23:59:59.999999 admitted; changing only hour24, minute60, second60 or microsecond1000000 returns its corresponding first error | leap-second60 rejected; uint16 fields are not signed negatives |
| T1 date/tick | tick0 decodes0001-01-01 and DayOfWeek returns1; tickD decodes0001-01-02 and returns2; re-encoding returns the respective tick | bounded day/epoch and weekday positive |
| T2 raw admission | greatest valid tick315537897599999999 decodes9999-12-31 23:59:59.999999; adding1 decodes10000-01-01, SetTick still0 but GetTick year error | return0 from SetTick is not date admission |
| T3 narrowed year | days to65537-01-01 =65536*365+65536/4-65536/100+65536/400=23936532 with integer quotients; tick2068116364800000000 narrows year65537 to1, giving0001-01-01 and GetTick0 | a valid resulting date does not prove preservation of the original raw tick |
| S1 whole seconds | SetTime_t0 decodes1970-01-01 atE;1 givesE+1000000 and one second later; validated GetTime_t returns0/1 | conditional nonnegative admitted whole-second inverse |
| S2 pre-epoch | date1969-12-31 23:59:59.999999 yieldsE-1 through GetTick, but GetTime_t returns0 just as1970-01-01; SetTime_t0 returns1970 | pre-epoch clamp is many-to-one, not negative Unix seconds |
| S3 fractions | dates represented byE+1 andE+999999 both GetTime_t0;E+1000000 returns1 | flooring loses subsecond identity; a seconds round-trip cannot retain it |
| S4 seconds intake | -1 returns raw32 INVALID_VALUE before write; accepted positive2^58 seconds scales by1000000=15625*2^6, so product is15625*2^64→0 modulo2^64, yieldingE/1970 | accepting a positive int64 is not an upper-bound/overflow guard |
| N1 now scale | supplied successful host sample sec0/nsec999 yieldsE; same sec/nsec1000 yieldsE+1; a failed uninitialized sample supplies no defined expected output | truncation and constant resolution are not an accuracy or host-success measurement |
| N2 caller offset | given nowE and CurrentClock minutes60, shifted tickE+3600000000 yields1970-01-01 01:00; minutes0 yields00:00 | explicit offset parameter, not host local timezone; export route limitation still applies |
| L1 stable offset | given O(u)=O(u+H)=H, H=3600000000 and representable u, UTC→local givesu+H, reverse givesu | equality requires the offset at both lookup arguments |
| L2 transition discriminator | given u=E+10D, O(u)=H but O(u+H)=2H, forward givesu+H and reverse givesu-H | hypothetical offset discontinuity disproves a general algebraic inverse; no actual timezone transition asserted |
| L3 local ambiguity | given O(a)=2H and O(a+H)=H, distinct UTCa and a+H both map toa+2H | one local scalar cannot retain both originals; actual zone/fold evidence remains absent |
| F1 format/capacity | under valid date/index/host/native-format premises, intended four-digit-year/two-digit-offset-hours text requires31+1=32 bytes; a31-byte caller span lacks capacity for the NUL | stack snprintf64 does not bound the caller destination; no overflow fixture executed |
| F2 format/index | admitted shifted year1970 yields an allowed weekday index; shifted raw tick for10000-01-01 yields year error from DayOfWeek used as index | raw tick→date0 cannot establish safe formatter indexing; stop before undefined access, no predicted string |
| P1 output phase | null GetTick/SetTick/offset pointers return pointer error before dereference/write; invalid GetTick date leaves an initialized tick sentinel unchanged; non-null invalid storage is not a defined error case | checked early error versus unchecked storage/fault and nontransactional writes |

## Reuse and next decision

**KNOWLEDGE_REFERENCE.** Original prose and arithmetic, no upstream code import. README declares GPL v2-or-later, LICENSE contains v2 text; selected RTC C file has no separate SPDX header, while the bbnet header explicitly identifies shadPS4 GPL-2.0-or-later. Preserve exact file/dependency licensing and lineage review before implementation reuse. Related forks/header copies and predecessor reviews are not independent RTC corroboration.

One controlling premise is missing: an attributable actual consumer with its selected callable ABI/host artifact, admitted raw input and destination capacity/identity, stable timezone basis and observed host/result phases. The [frontier](../frontiers/rtc-conversion.md) gives a bounded future discriminator, branches and stop rule; it grants no execution. No serialized data, native fixture, original/private/game/save input, runtime/device/UI/timing or game/fidelity/usability evidence exists here. Issue #9 remains OPEN / NOT MET; earlier failed answers, grades and evaluated heads remain immutable. No reader retry.

[rtc]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime_rtc.c
[runtime]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.c
[header]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/runtime.h
[names]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/import_names.inc
[probe]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/src/probe.c
[shim]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/shim/bbgpu.cpp
[netheader]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/bbnet/include/core/libraries/rtc/rtc.h
[build]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/build.sh
[readme]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/README.md
[license]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/LICENSE
[vendor]: https://github.com/deadinside28/bloodborne_pc/blob/3c57da4198ad62039f63f33bfd205b9916518acf/gpu/VENDOR.txt
